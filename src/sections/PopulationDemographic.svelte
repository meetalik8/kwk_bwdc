<script>
  import { onMount } from "svelte";
  import Highcharts from "highcharts";
  import Scroller from "../lib/Scroller.svelte";
  import ObservedArticleText from "../lib/ObservedArticleText.svelte";
  let chart;

  const data = [
    { group: "Black", georgia: 31.3, fulton: 43.1 },
    { group: "Asian", georgia: 4.4, fulton: 7.6 },
    { group: "White", georgia: 52.5, fulton: 39.4 },
  ];
  const options = {
    threshold: [0.85, 0.95],
  };
  const chartOptions = {
    chart: {
      type: "column",
      backgroundColor: "transparent",
      plotBackgroundColor: "transparent",
    },
    title: { text: null },
    xAxis: {
      categories: data.map((d) => d.group),
      crosshair: true,
    },
    yAxis: {
      min: 0,
      title: { text: "Population (%)" },
    },
    series: [
      {
        name: "Georgia",
        data: data.map((d) => d.georgia),
        color: "#4572A7",
      },
      {
        name: "Fulton County",
        data: data.map((d) => d.fulton),
        color: "#AA4643",
      },
    ],
    legend: { enabled: true },
    credits: { enabled: false },
  };

  onMount(() => {
    chart = Highcharts.chart("bar-chart", chartOptions);
  });

  let slides;
  onMount(() => {
    slides = document.querySelectorAll(".text-slide");
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add("visible");
          }
        });
      },
      { threshold: 0.5 }
    );

    slides.forEach((slide) => observer.observe(slide));
  });
  let chartContainer;

  onMount(() => {
    chart = Highcharts.chart("bar-chart", chartOptions);

    slides = document.querySelectorAll(".text-slide");
    const observer = new IntersectionObserver(callback, options);
    slides.forEach((slide) => observer.observe(slide));

    const chartObserver = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            chartContainer.classList.remove("hidden");
            chartContainer.classList.add("fade-in");
            chart.update();
          }
        });
      },
      { threshold: 0.5 }
    );

    if (chartContainer) {
      chartObserver.observe(chartContainer);
    }
  });

  const callback = (entries, observer) => {
    entries.forEach((entry) => {
      const elem = entry.target;

      if (entry.intersectionRatio >= 0.9) {
        // "active" state
        elem.style.backgroundColor = "rgba(252, 255, 254, 0.75)";
      } else if (entry.intersectionRatio < 0.9) {
        // "inactive" state
        elem.style.backgroundColor = "rgba(106, 62, 55, 0.75)";
      }
    });
  };
</script>

<section class="lead-in">
  <div class="overlay-text">
    <h1>
      To understand access, we must first understand who calls Georgia home.
    </h1>
  </div>
</section>

<div>
  <Scroller layout="right">
    {#snippet sticky()}
      <h2><strong>Who lives in Georgia?</strong></h2>
      <div class="chart-container hidden" bind:this={chartContainer}>
        <div id="bar-chart"></div>
      </div>
    {/snippet}

    {#snippet scrolly()}
      <ObservedArticleText class="text-slide" {callback} {options}>
        <h2>Georgia: A Diverse State</h2>
        <p>
          Georgia's population is predominantly White, but also features a
          significant Black community. Asian residents make up a smaller yet
          growing share of the population.
        </p>
      </ObservedArticleText>

      <ObservedArticleText class="text-slide" {callback} {options}>
        <h2>Now, Let's Zoom In</h2>
        <p>
          Fulton County, home to Atlanta, reflects a different picture. The
          Black population here is larger than the state average, and the Asian
          community is more prominent too.
        </p>
      </ObservedArticleText>

      <ObservedArticleText class="text-slide" {callback} {options}>
        <h2>State vs. County</h2>
        <p>
          Compared to Georgia as a whole, Fulton County has fewer White
          residents, and noticeably more Black and Asian residents. This paints
          a unique demographic story within the state.
        </p>
      </ObservedArticleText>
    {/snippet}
  </Scroller>
</div>

<style>
  .lead-in {
    height: 100vh;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    overflow: hidden;
    font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
  }

  .overlay-text {
    background: rgba(0, 0, 0, 0.6);
    padding: 3rem;
    border-radius: 16px;
    max-width: 800px;
    color: white;
    text-align: center;
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.1);
  }

  .overlay-text h1 {
    font-size: 2.8rem;
    line-height: 1.3;
    margin: 0;
    font-weight: 700;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    letter-spacing: -0.02em;
  }

  .chart-container {
    width: 90%;
    max-width: 900px;
    height: auto;
    padding: 2.5rem 2rem;
    display: flex;
    align-items: center;
    justify-content: center;
    background: white;
    border-radius: 16px;
    box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1), 0 4px 6px -1px rgba(0, 0, 0, 0.06);
    border: 1px solid rgba(226, 232, 240, 0.8);
    transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .chart-container.hidden {
    opacity: 0;
    transform: translateY(50px) scale(0.95);
  }

  #bar-chart {
    width: 100%;
    height: 380px;
  }

  h2 {
    font-size: 2.2rem;
    margin-bottom: 1.5rem;
    text-align: center;
    color: #1e293b;
    font-weight: 700;
    font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
    letter-spacing: -0.02em;
  }

  p {
    font-size: 1.15rem;
    line-height: 1.7;
    max-width: 520px;
    margin: 0 auto 2rem auto;
    color: #475569;
    font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
    font-weight: 400;
    transition: all 0.6s ease;
  }

  /* Text slide animations and states */
  :global(.text-slide) {
    padding: 2rem;
    border-radius: 12px;
    margin-bottom: 2rem;
    transition: all 0.4s ease;
    backdrop-filter: blur(10px);
  }

  :global(.text-slide.visible) {
    transform: translateX(0);
    opacity: 1;
  }

  /* Responsive design */
  @media (max-width: 768px) {
    .overlay-text {
      padding: 2rem;
      margin: 1rem;
    }

    .overlay-text h1 {
      font-size: 2.2rem;
    }

    .chart-container {
      padding: 1.5rem 1rem;
      margin: 0 1rem;
    }

    #bar-chart {
      height: 300px;
    }

    h2 {
      font-size: 1.8rem;
    }

    p {
      font-size: 1rem;
      max-width: 90%;
    }
  }

  @media (max-width: 480px) {
    .overlay-text h1 {
      font-size: 1.8rem;
    }

    h2 {
      font-size: 1.5rem;
    }

    .chart-container {
      padding: 1rem;
    }

    #bar-chart {
      height: 250px;
    }
  }
</style>