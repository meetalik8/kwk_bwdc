<script>
  import * as Highcharts from "highcharts";
  import { Chart } from "@highcharts/svelte";
  import Scroller from "../lib/Scroller.svelte";
  import ArticleText from "../lib/ArticleText.svelte";

  let options = {
    chart: {
      type: "column",
      backgroundColor: "transparent"
    },
    title: {
      text: "Bachelor's Degree Attainment by Race (%)"
    },
    xAxis: {
      categories: ['Black', 'Asian', 'White'],
      title: {
        text: 'Race'
      }
    },
    yAxis: {
      min: 0,
      max: 100,
      title: {
        text: 'Percent with Bachelor&apos;s Degree'
      }
    },
    legend: {
      align: 'center',
      verticalAlign: 'bottom'
    },
    tooltip: {
      shared: true,
      valueSuffix: '%'
    },
    plotOptions: {
      column: {
        dataLabels: {
          enabled: true,
          format: '{y}%'
        }
      }
    },
    series: [
      {
        name: 'Georgia',
        data: [27.4, 59.0, 37.3],
        color: '#4572A7'
      },
      {
        name: 'Fulton County',
        data: [37.5, 82.3, 75.4],
        color: '#AA4643'
      }
    ]
  };
</script>

<section class="lead-in">
  <div class="overlay-text">
    <h1>
      To understand opportunity, we must first understand who has access to higher education.
    </h1>
  </div>
</section>

<div>
  <Scroller layout="left">
    {#snippet sticky()}
      <h2><strong>Education Disparities Across Race</strong></h2>
      <div class="chart-container">
        <div class="chart">
          <Chart {options} highcharts={Highcharts} />
        </div>
      </div>
    {/snippet}

    {#snippet scrolly()}
      <ArticleText>
        In Georgia, only <strong>27.4%</strong> of the Black population has a bachelor's degree,
        compared to <strong>59.0%</strong> of Asians and <strong>37.3%</strong> of Whites.
      </ArticleText>

      <ArticleText>
        Fulton County, while more educated overall, reflects similar trends:
        <strong>82.3%</strong> of Asians and <strong>75.4%</strong> of Whites have degrees,
        while only <strong>37.5%</strong> of Black residents do.
      </ArticleText>

      <ArticleText>
        The racial gap in educational attainment is stark. While geography improves overall
        education levels, it does not erase systemic disparities.
      </ArticleText>

      <ArticleText>
        These gaps can have long-term impacts on economic mobility, access to leadership roles,
        and wealth accumulation in certain communities.
      </ArticleText>
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
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 1rem;
  }

  .chart {
    width: 90%;
    max-width: 900px;
    background: white;
    border-radius: 16px;
    padding: 2.5rem 2rem;
    box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1), 0 4px 6px -1px rgba(0, 0, 0, 0.06);
    border: 1px solid rgba(226, 232, 240, 0.8);
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }

  .chart::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 4px;
    background: linear-gradient(90deg, #3b82f6, #06b6d4);
    opacity: 0.8;
  }

  .chart:hover {
    transform: translateY(-2px);
    box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
  }

  h2 {
    font-size: 2.2rem;
    margin-bottom: 2rem;
    text-align: center;
    color: #1e293b;
    font-weight: 700;
    font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
    letter-spacing: -0.02em;
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

    .chart {
      width: 95%;
      padding: 2rem 1.5rem;
    }

    h2 {
      font-size: 1.8rem;
      margin-bottom: 1.5rem;
    }

    :global(.article-text) {
      width: 85%;
      padding: 2rem;
      margin: 40vh auto;
      font-size: 1rem;
    }
  }

  @media (max-width: 480px) {
    .overlay-text h1 {
      font-size: 1.8rem;
    }

    .chart {
      width: 98%;
      padding: 1.5rem 1rem;
    }

    h2 {
      font-size: 1.5rem;
    }

    :global(.article-text) {
      width: 90%;
      padding: 1.5rem;
      font-size: 0.95rem;
    }
  }
</style>