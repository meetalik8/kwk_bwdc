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
  let currentSlide = 0;

  const updateChart = (index) => {
    currentSlide = index;

    if (chart) {
      const updatedSeries = [
        {
          name: "Georgia",
          data: data.map((d) => (index >= 1 ? d.georgia : 0)),
          color: "#1E91D6",
        },
        {
          name: "Fulton County",
          data: data.map((d) => (index >= 2 ? d.fulton : 0)),
          color: "#CC2936",
        },
      ];

      chart.update({
        series: updatedSeries,
      });
    }
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
          Georgia’s population is predominantly White, but also features a
          significant Black community. Asian residents make up a smaller yet
          growing share of the population.
        </p>
      </ObservedArticleText>

      <ObservedArticleText class="text-slide" {callback} {options}>
        <h2>Now, Let’s Zoom In</h2>
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

  .chart-container {
    width: 90%;
    max-width: 900px;
    height: auto;
    padding: 2rem 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: white;
  }
  .lead-in {
    height: 100vh;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    overflow: hidden;
  }
  .overlay-text h1 {
    font-size: 2.5rem;
    line-height: 1.4;
    margin-bottom: 2rem;
    font-weight: 700;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  }

  #bar-chart {
    width: 100%;
    height: 320px;
  }

  h2 {
    font-size: 2rem;
    margin-bottom: 1rem;
    text-align: center;
    color: #222;
  }

  p {
    font-size: 1.1rem;
    line-height: 1.6;
    max-width: 500px;
    margin: 0 auto 2rem auto;
    color: #333;
    transition: opacity 0.6s ease-in-out;
  }

  .overlay-text {
    background: rgba(0, 0, 0, 0.6);
    padding: 2rem;
    border-radius: 12px;
    max-width: 700px;
    color: white;
    text-align: center;
  }

  .overlay-text h1 {
    font-size: 2rem;
    line-height: 1.5;
  }

  .chart-container.hidden {
    opacity: 0;
    transform: translateY(40px);
    transition:
      opacity 1s ease,
      transform 1s ease;
  }

  .chart-container {
    width: 90%;
    max-width: 900px;
    height: auto;
    padding: 2rem 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: white;
    border-radius: 12px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
  }

  #bar-chart {
    width: 100%;
    height: 320px;
  }
</style>
