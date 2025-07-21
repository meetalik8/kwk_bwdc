<script>
  import * as Highcharts from "highcharts";
  import { Chart } from "@highcharts/svelte";
  import Scroller from "../lib/Scroller.svelte";
  import ArticleText from "../lib/ArticleText.svelte";


  const nationalOccupationOptions = {
    chart: {
      type: "pie",
      backgroundColor: "transparent"
    },
    title: {
      text: "National Representation: Management & Professional Roles"
    },
    tooltip: {
      pointFormat: "{series.name}: <b>{point.percentage:.1f}%</b>"
    },
    plotOptions: {
      pie: {
        allowPointSelect: true,
        cursor: "pointer",
        dataLabels: {
          enabled: true,
          format: "<b>{point.name}</b>: {point.percentage:.1f} %"
        }
      }
    },
    series: [
      {
        name: "Share",
        colorByPoint: true,
        data: [
          { name: "Black", y: 18.14, color: "#1f78b4" },
          { name: "Asian", y: 33.77, color: "#33a02c" },
          { name: "White", y: 25.63, color: "#ff7f00" }
        ]
      }
    ]
  };
</script>

<section class="lead-in">
  <div class="overlay-text">
    <h1>
      To understand power, we must examine who holds leadership positions and who’s left out.
    </h1>
  </div>
</section>

<Scroller layout="right">
  {#snippet sticky()}
    <h2><strong>Who Gets to Lead?</strong></h2>
    <div class="chart-container">
      <div class="chart">
        <Chart options={nationalOccupationOptions} highcharts={Highcharts} />
      </div>
    </div>
  {/snippet}

  {#snippet scrolly()}
    <ArticleText >
      Leadership roles in management, business, and professional fields shape the access to power and wealth.
    </ArticleText>

    <ArticleText >
      At the <strong>national level</strong>, <strong>Asians</strong> lead this category with <strong>33.77%</strong> representation show
      a significant presence in high-skill sectors despite being a smaller population group.
    </ArticleText>

    <ArticleText>
      <strong>White individuals</strong> hold <strong>25.63%</strong> of these roles showing broad access to leadership but not the highest share.
    </ArticleText>

    <ArticleText>
      <strong>Black workers</strong>, by contrast, represent just <strong>18.14%</strong> exposing a sharp underrepresentation in roles that typically lead to decision-making power and upward mobility.
    </ArticleText>
  {/snippet}
</Scroller>

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
    .chart {
      width: 95%;
      padding: 2rem 1.5rem;
    }

    h2 {
      font-size: 1.8rem;
      margin-bottom: 1.5rem;
    }
  }

  @media (max-width: 480px) {
    .chart {
      width: 98%;
      padding: 1.5rem 1rem;
    }

    h2 {
      font-size: 1.5rem;
    }
  }
</style>