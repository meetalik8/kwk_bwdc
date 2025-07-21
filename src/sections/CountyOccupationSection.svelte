<script>
  import * as Highcharts from "highcharts";
  import { Chart } from "@highcharts/svelte";
  import Scroller from "../lib/Scroller.svelte";
  import ArticleText from "../lib/ArticleText.svelte";

  const fultonOptions = {
    chart: {
      type: "pie",
      backgroundColor: "transparent"
    },
    title: {
      text: "Fulton County: Leadership Roles by Race & Gender"
    },
    tooltip: {
      pointFormat: '{series.name}: <b>{point.percentage:.1f}%</b>'
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
    series: [{
      name: "Share",
      colorByPoint: true,
      data: [
        { name: "White Male", y: 55.14, color: "#ff7f00" },
        { name: "White Female", y: 43.16, color: "#fdbf6f" },
        { name: "Black Male", y: 22.12, color: "#1f78b4" },
        { name: "Black Female", y: 34.13, color: "#a6cee3" },
        { name: "Asian Male", y: 12.85, color: "#33a02c" },
        { name: "Asian Female", y: 8.62, color: "#b2df8a" }
      ]
    }]
  };
</script>
<Scroller layout="right">
  {#snippet sticky()}
    <h2><strong>Zooming In: Fulton County</strong></h2>
    <div class="chart">
      <Chart options={fultonOptions} highcharts={Highcharts} />
    </div>
  {/snippet}

  {#snippet scrolly()}
    <ArticleText>
      In Fulton County, the racial and gender dynamics of leadership roles differ from the state. <strong>White men</strong> lead with <strong>55.1%</strong> of top roles, followed by <strong>White women</strong> at <strong>43.2%</strong>, despite White residents making up less than 40% of the population.
    </ArticleText>

    <ArticleText>
      <strong>Black women</strong> hold <strong>34.1%</strong> of management and professional roles—higher than <strong>Black men</strong> at <strong>22.1%</strong>. This is notable given Black residents are the largest racial group in Fulton and more Black women hold degrees than men.
    </ArticleText>

    <ArticleText>
      <strong>Asian men</strong> and <strong>Asian women</strong> account for <strong>12.9%</strong> and <strong>8.6%</strong> respectively. Asians make up only <strong>7.6%</strong> of the population, but their <strong>82.3%</strong> bachelor's degree attainment fuels their visibility in leadership.
    </ArticleText>

    <ArticleText>
      Fulton shows a more diverse leadership profile than Georgia overall. Still, White men dominate, and the race-gender gap persists across sectors of power.
    </ArticleText>
  {/snippet}
</Scroller>

<style>
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
