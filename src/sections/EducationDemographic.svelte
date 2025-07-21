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
      text: "Bachelor’s Degree Attainment by Race (%)"
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
        text: 'Percent with Bachelor’s Degree'
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
      <div class="chart">
        <Chart {options} highcharts={Highcharts} />
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
        and wealth accumulation in communities of color.
      </ArticleText>

    {/snippet}
  </Scroller>
</div>

<style>
  .chart {
    width: 90%;
    margin: 0px auto;
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
  .overlay-text {
    background: rgba(0, 0, 0, 0.6);
    padding: 2rem;
    border-radius: 12px;
    max-width: 700px;
    color: white;
    text-align: center;
  }


  @keyframes blink-caret {
    0%, 100% {
      border-color: transparent;
    }
    50% {
      border-color: rgba(255, 255, 255, 0.6);
    }
  }
</style>
