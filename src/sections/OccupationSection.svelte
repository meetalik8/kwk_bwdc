<script>
	import * as Highcharts from "highcharts";
	import { Chart } from "@highcharts/svelte";
	import Scroller from "../lib/Scroller.svelte";
	import ArticleText from "../lib/ArticleText.svelte";

	let nationalOptions = {
		chart: {
			type: 'pie',
			backgroundColor: 'transparent'
		},
		title: { text: "National Employment in Management & Related Professions" },
		tooltip: {
			pointFormat: '{series.name}: <b>{point.percentage:.1f}%</b>'
		},
		plotOptions: {
			pie: {
				allowPointSelect: true,
				cursor: 'pointer',
				dataLabels: {
					enabled: true,
					format: '<b>{point.name}</b>: {point.percentage:.1f} %'
				}
			}
		},
		series: [{
			name: 'Share',
			colorByPoint: true,
			data: [
				{ name: 'Black', y: 18.14, color: '#1f78b4' },
				{ name: 'Asian', y: 33.77, color: '#33a02c' },
				{ name: 'White', y: 25.63, color: '#ff7f00' }
			]
		}]
	};

	let georgiaOptions = {
		chart: {
			type: 'pie',
			backgroundColor: 'transparent'
		},
		title: { text: "Georgia Employment Distribution by Race & Gender" },
		tooltip: {
			pointFormat: '{series.name}: <b>{point.percentage:.1f}%</b>'
		},
		plotOptions: {
			pie: {
				allowPointSelect: true,
				cursor: 'pointer',
				dataLabels: {
					enabled: true,
					format: '<b>{point.name}</b>: {point.percentage:.1f} %'
				}
			}
		},
		series: [{
			name: 'Share',
			colorByPoint: true,
			data: [
				{ name: 'White Male', y: 59.48, color: '#ff7f00' },
				{ name: 'White Female', y: 52.31, color: '#fdbf6f' },
				{ name: 'Black Male', y: 18.56, color: '#1f78b4' },
				{ name: 'Black Female', y: 28.33, color: '#a6cee3' },
				{ name: 'Asian Male', y: 7.87, color: '#33a02c' },
				{ name: 'Asian Female', y: 5.13, color: '#b2df8a' }
			]
		}]
	};

	let fultonOptions = {
		chart: {
			type: 'pie',
			backgroundColor: 'transparent'
		},
		title: { text: "Fulton County Employment Distribution by Race & Gender" },
		tooltip: {
			pointFormat: '{series.name}: <b>{point.percentage:.1f}%</b>'
		},
		plotOptions: {
			pie: {
				allowPointSelect: true,
				cursor: 'pointer',
				dataLabels: {
					enabled: true,
					format: '<b>{point.name}</b>: {point.percentage:.1f} %'
				}
			}
		},
		series: [{
			name: 'Share',
			colorByPoint: true,
			data: [
				{ name: 'White Male', y: 55.14, color: '#ff7f00' },
				{ name: 'White Female', y: 43.16, color: '#fdbf6f' },
				{ name: 'Black Male', y: 22.12, color: '#1f78b4' },
				{ name: 'Black Female', y: 34.13, color: '#a6cee3' },
				{ name: 'Asian Male', y: 12.85, color: '#33a02c' },
				{ name: 'Asian Female', y: 8.62, color: '#b2df8a' }
			]
		}]
	};
</script>

<Scroller layout="left">
	{#snippet sticky()}
		<h2><strong>Who Gets to Lead?</strong></h2>
		<div class="chart"><Chart options={nationalOptions} highcharts={Highcharts} /></div>
	{/snippet}

	{#snippet scrolly()}
		<ArticleText>
			At the national level, <strong>Asians</strong> are the most represented in management and related professions,
			followed by <strong>Whites</strong> and <strong>Black</strong> individuals.
		</ArticleText>

		<ArticleText>
			Zooming into <strong>Georgia</strong>, we see how race and gender interact.
			White men are most dominant in leadership roles, while Asian women have the lowest share.
		</ArticleText>

		<div class="chart"><Chart options={georgiaOptions} highcharts={Highcharts} /></div>

		<ArticleText>
			Looking even closer, <strong>Fulton County</strong> presents a slightly more diverse picture.
			Black women lead more than Black men — but White men still dominate.
		</ArticleText>

		<div class="chart"><Chart options={fultonOptions} highcharts={Highcharts} /></div>
	{/snippet}
</Scroller>

<style>
	.chart {
		width: 90%;
		max-width: 600px;
		margin: 2rem auto;
	}
	h2 {
		background-color: rgba(3, 76, 54, 0.9);
		color: white;
		padding: 1rem;
		border-radius: 1rem;
		box-shadow: 6px 6px #188f70;
	}
</style>
