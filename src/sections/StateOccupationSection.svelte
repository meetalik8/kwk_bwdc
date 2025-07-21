<script>
  import * as Highcharts from "highcharts";
  import { Chart } from "@highcharts/svelte";
  import Scroller from "../lib/Scroller.svelte";
  import ArticleText from "../lib/ArticleText.svelte";

  const georgiaOccupationOptions = {
    chart: {
      type: "pie",
      backgroundColor: "transparent"
    },
    title: {
      text: "Georgia: Leadership Representation by Race & Gender"
    },
    tooltip: {
      pointFormat: "{series.name}: <b>{point.percentage:.2f}%</b>"
    },
    plotOptions: {
      pie: {
        allowPointSelect: true,
        cursor: "pointer",
        dataLabels: {
          enabled: true,
          format: "<b>{point.name}</b>: {point.percentage:.2f} %"
        }
      }
    },
    series: [
      {
        name: "Share",
        colorByPoint: true,
        data: [
          { name: "White Male", y: 59.48, color: "#ff7f00" },
          { name: "White Female", y: 52.31, color: "#fdbf6f" },
          { name: "Black Male", y: 18.56, color: "#1f78b4" },
          { name: "Black Female", y: 28.33, color: "#a6cee3" },
          { name: "Asian Male", y: 7.87, color: "#33a02c" },
          { name: "Asian Female", y: 5.13, color: "#b2df8a" }
        ]
      }
    ]
  };
</script>

<!-- Georgia Occupation Section -->
<Scroller layout="left">
  {#snippet sticky()}
    <h2><strong>Zooming In: Georgia</strong></h2>
    <div class="chart">
      <Chart options={georgiaOccupationOptions} highcharts={Highcharts} />
    </div>
  {/snippet}

  {#snippet scrolly()}
<ArticleText>
  Georgia’s population is roughly <strong>51% White</strong>, <strong>33% Black</strong>, and <strong>4.4% Asian</strong>. These proportions provide a baseline for understanding representation in leadership roles.
</ArticleText>

<ArticleText>
  <strong>White men</strong> hold nearly <strong>59.5%</strong> of management and professional occupations, which exceeds their population share. <strong>White women</strong> are also highly represented, holding <strong>52.3%</strong> of these roles.
</ArticleText>

<ArticleText>
  <strong>Black men</strong> and <strong>Black women</strong> collectively hold less than <strong>47%</strong> of such positions, despite being over a third of the population. Notably, Black women hold a larger share than Black men, at <strong>28.3%</strong> and <strong>18.6%</strong> respectively.
</ArticleText>

<ArticleText>
  <strong>Asian men</strong> and <strong>Asian women</strong> hold <strong>7.9%</strong> and <strong>5.1%</strong> of leadership roles. This is significantly lower than expected, especially considering Asians have the highest bachelor’s degree attainment rate in the state at <strong>59%</strong>.
</ArticleText>

<ArticleText>
  The gap between educational qualifications and occupational representation suggests that formal education alone does not ensure equal access to leadership opportunities. Structural barriers continue to shape who gets to lead.
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
