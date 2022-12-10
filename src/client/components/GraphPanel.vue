<template>
  <div id="graph-panel">
        <h2>Generational Stats</h2>
        <canvas id="points-chart-VPTotal" style="width: 750px; height: 400px; display: inline;"></canvas>
        <canvas id="points-chart-VPCards" style="width: 750px; height: 400px; display: inline;"></canvas>
        <canvas id="points-chart-TR" style="width: 750px; height: 400px; display: inline;"></canvas>
        <canvas id="points-chart-City" style="width: 750px; height: 400px; display: inline;"></canvas>
        <canvas id="points-chart-Green" style="width: 750px; height: 400px; display: inline;"></canvas>
        <canvas id="points-chart-Milestone" style="width: 750px; height: 400px; display: inline;"></canvas>
        <canvas id="points-chart-Award" style="width: 750px; height: 400px; display: inline;"></canvas>
        <canvas id="points-chart-EV" style="width: 750px; height: 400px; display: inline;"></canvas>
        <canvas id="points-chart-MoonCol" style="width: 750px; height: 400px; display: inline;"></canvas>
        <canvas id="points-chart-MoonMine" style="width: 750px; height: 400px; display: inline;"></canvas>
        <canvas id="points-chart-MoonRoad" style="width: 750px; height: 400px; display: inline;"></canvas>
        <canvas id="points-chart-Planet" style="width: 750px; height: 400px; display: inline;"></canvas>
    </div>
</template>

<script lang="ts">

import Vue from 'vue';
// const Chart = require('chart.js');
import {Chart, registerables} from 'chart.js';
Chart.register(...registerables);
import {PublicPlayerModel} from '@/common/models/PlayerModel';


export default Vue.extend({
  name: 'graph-panel',
  props: {
    players: {
      type: Array as () => Array<PublicPlayerModel>,
    },
  },
  computed: {
  },
  data() {
    return {
    };
  },
  methods: {
    getSortedPlayers() {
      const copy = [...this.players];
      copy.sort(function(a:PublicPlayerModel, b:PublicPlayerModel) {
        if (a.victoryPointsBreakdown.total < b.victoryPointsBreakdown.total) return -1;
        if (a.victoryPointsBreakdown.total > b.victoryPointsBreakdown.total) return 1;
        if (a.megaCredits < b.megaCredits) return -1;
        if (a.megaCredits > b.megaCredits) return 1;
        return 0;
      });
      return copy.reverse();
    },
    updateCharts() {
      const colorCode = {'red': 'rgb(153, 17, 0)',
        'green': 'rgb(0, 153, 0)',
        'yellow': 'rgb(170, 170, 0)',
        'blue': 'rgb(0, 102, 255)',
        'black': 'rgb(170, 170, 170)',
        'purple': 'rgb(140, 0, 255)',
        'orange': 'rgb(236, 113, 12)',
        'pink': 'rgb(245, 116, 187)',
        'neutral': 'rbg(68, 68, 68)',
        'bronze': 'rbg(205, 127, 50)'};
      Chart.defaults.font.family = 'Ubuntu';
      Chart.defaults.color = '#ddd';
      const chartData: {type: String, data: {labels: Number[], datasets: {label: String, data: Number[], borderColor: String, tension: Number}[]}, options: {responsive: boolean, scales: {yAxes: {beginAtZero: boolean, ticks: {font: {size: Number}, callback(value: number): number | undefined}, title: {display: boolean, text: String, font: {size: number}}}, xAxes: {ticks: {font: {size: number}}, title: {display: boolean, text: String, font: {size: number}}}}, plugins: {title: {display: boolean, text: String, font: {size: number}}, legend: {labels: {font: {size: number}}}}}}[] = [
        {type: 'line', data: {labels: [], datasets: []}, options: {responsive: false, scales: {yAxes: {beginAtZero: true, ticks: {font: {size: 18}, callback: function(value) {
          if (Math.floor(+value) === value) {
            return value;
          } return undefined;
        }}, title: {display: true, text: '', font: {size: 18}}}, xAxes: {ticks: {font: {size: 18}}, title: {display: true, text: 'Generation', font: {size: 18}}}}, plugins: {title: {display: true, text: '', font: {size: 24}}, legend: {labels: {font: {size: 18}}}}}},
        {type: 'line', data: {labels: [], datasets: []}, options: {responsive: false, scales: {yAxes: {beginAtZero: true, ticks: {font: {size: 18}, callback: function(value) {
          if (Math.floor(+value) === value) {
            return value;
          } return undefined;
        }}, title: {display: true, text: '', font: {size: 18}}}, xAxes: {ticks: {font: {size: 18}}, title: {display: true, text: 'Generation', font: {size: 18}}}}, plugins: {title: {display: true, text: '', font: {size: 24}}, legend: {labels: {font: {size: 18}}}}}},
        {type: 'line', data: {labels: [], datasets: []}, options: {responsive: false, scales: {yAxes: {beginAtZero: true, ticks: {font: {size: 18}, callback: function(value) {
          if (Math.floor(+value) === value) {
            return value;
          } return undefined;
        }}, title: {display: true, text: '', font: {size: 18}}}, xAxes: {ticks: {font: {size: 18}}, title: {display: true, text: 'Generation', font: {size: 18}}}}, plugins: {title: {display: true, text: '', font: {size: 24}}, legend: {labels: {font: {size: 18}}}}}},
        {type: 'line', data: {labels: [], datasets: []}, options: {responsive: false, scales: {yAxes: {beginAtZero: true, ticks: {font: {size: 18}, callback: function(value) {
          if (Math.floor(+value) === value) {
            return value;
          } return undefined;
        }}, title: {display: true, text: '', font: {size: 18}}}, xAxes: {ticks: {font: {size: 18}}, title: {display: true, text: 'Generation', font: {size: 18}}}}, plugins: {title: {display: true, text: '', font: {size: 24}}, legend: {labels: {font: {size: 18}}}}}},
        {type: 'line', data: {labels: [], datasets: []}, options: {responsive: false, scales: {yAxes: {beginAtZero: true, ticks: {font: {size: 18}, callback: function(value) {
          if (Math.floor(+value) === value) {
            return value;
          } return undefined;
        }}, title: {display: true, text: '', font: {size: 18}}}, xAxes: {ticks: {font: {size: 18}}, title: {display: true, text: 'Generation', font: {size: 18}}}}, plugins: {title: {display: true, text: '', font: {size: 24}}, legend: {labels: {font: {size: 18}}}}}},
        {type: 'line', data: {labels: [], datasets: []}, options: {responsive: false, scales: {yAxes: {beginAtZero: true, ticks: {font: {size: 18}, callback: function(value) {
          if (Math.floor(+value) === value) {
            return value;
          } return undefined;
        }}, title: {display: true, text: '', font: {size: 18}}}, xAxes: {ticks: {font: {size: 18}}, title: {display: true, text: 'Generation', font: {size: 18}}}}, plugins: {title: {display: true, text: '', font: {size: 24}}, legend: {labels: {font: {size: 18}}}}}},
        {type: 'line', data: {labels: [], datasets: []}, options: {responsive: false, scales: {yAxes: {beginAtZero: true, ticks: {font: {size: 18}, callback: function(value) {
          if (Math.floor(+value) === value) {
            return value;
          } return undefined;
        }}, title: {display: true, text: '', font: {size: 18}}}, xAxes: {ticks: {font: {size: 18}}, title: {display: true, text: 'Generation', font: {size: 18}}}}, plugins: {title: {display: true, text: '', font: {size: 24}}, legend: {labels: {font: {size: 18}}}}}},
        {type: 'line', data: {labels: [], datasets: []}, options: {responsive: false, scales: {yAxes: {beginAtZero: true, ticks: {font: {size: 18}, callback: function(value) {
          if (Math.floor(+value) === value) {
            return value;
          } return undefined;
        }}, title: {display: true, text: '', font: {size: 18}}}, xAxes: {ticks: {font: {size: 18}}, title: {display: true, text: 'Generation', font: {size: 18}}}}, plugins: {title: {display: true, text: '', font: {size: 24}}, legend: {labels: {font: {size: 18}}}}}},
        {type: 'line', data: {labels: [], datasets: []}, options: {responsive: false, scales: {yAxes: {beginAtZero: true, ticks: {font: {size: 18}, callback: function(value) {
          if (Math.floor(+value) === value) {
            return value;
          } return undefined;
        }}, title: {display: true, text: '', font: {size: 18}}}, xAxes: {ticks: {font: {size: 18}}, title: {display: true, text: 'Generation', font: {size: 18}}}}, plugins: {title: {display: true, text: '', font: {size: 24}}, legend: {labels: {font: {size: 18}}}}}},
        {type: 'line', data: {labels: [], datasets: []}, options: {responsive: false, scales: {yAxes: {beginAtZero: true, ticks: {font: {size: 18}, callback: function(value) {
          if (Math.floor(+value) === value) {
            return value;
          } return undefined;
        }}, title: {display: true, text: '', font: {size: 18}}}, xAxes: {ticks: {font: {size: 18}}, title: {display: true, text: 'Generation', font: {size: 18}}}}, plugins: {title: {display: true, text: '', font: {size: 24}}, legend: {labels: {font: {size: 18}}}}}},
        {type: 'line', data: {labels: [], datasets: []}, options: {responsive: false, scales: {yAxes: {beginAtZero: true, ticks: {font: {size: 18}, callback: function(value) {
          if (Math.floor(+value) === value) {
            return value;
          } return undefined;
        }}, title: {display: true, text: '', font: {size: 18}}}, xAxes: {ticks: {font: {size: 18}}, title: {display: true, text: 'Generation', font: {size: 18}}}}, plugins: {title: {display: true, text: '', font: {size: 24}}, legend: {labels: {font: {size: 18}}}}}},
        {type: 'line',
          data: {
            labels: [],
            datasets: [],
          },
          options: {
            responsive: false,
            scales: {
              yAxes: {
                beginAtZero: true,
                ticks: {
                  font: {
                    size: 18,
                  },
                  callback: function(value) {
                    if (Math.floor(+value) === value) {
                      return value;
                    }
                    return undefined;
                  },
                },
                title: {
                  display: true,
                  text: '',
                  font: {
                    size: 18,
                  },
                },
              },
              xAxes: {
                ticks: {
                  font: {
                    size: 18,
                  },
                },
                title: {
                  display: true,
                  text: 'Generation',
                  font: {
                    size: 18,
                  },
                },
              },
            },
            plugins: {
              title: {
                display: true,
                text: '',
                font: {
                  size: 24,
                },
              },
              legend: {
                labels: {
                  font: {
                    size: 18,
                  },
                },
              },
            },
          },
        },
      ];


      const gens = Math.max(...Object.keys(this.players[0].victoryPointsBreakdownHistory).map((gen) => {
        return Number(gen);
      }));
      chartData.forEach((_, i) => chartData[i].data.labels = Array.from({length: gens}, (_, k)=>k+1));

      this.getSortedPlayers().forEach((player) => {
        const hist = player.victoryPointsBreakdownHistory;
        const playerData: {label: String, data: Number[], borderColor: String, backgroundColor: String, tension: Number}[] = [];
        for (let i = 0; i < 12; i++) {
          playerData.push({label: player.name, data: [], borderColor: colorCode[player.color], backgroundColor: colorCode[player.color], tension: 0});
        }

        const categories = ['terraformRating', 'milestones', 'awards', 'greenery', 'city', 'escapeVelocity', 'moonHabitats', 'moonMines', 'moonRoads', 'planetaryTracks', 'victoryPoints', 'total'];
        const categoryLabels = {'terraformRating': 'Terraform Rating', 'milestones': 'Milestone Points', 'awards': 'Award Points', 'greenery': 'Greeneries', 'city': 'City Points', 'escapeVelocity': 'Escape Velocity', 'moonHabitats': 'Moon Colony Points', 'moonMines': 'Moon Mine Points', 'moonRoads': 'Moon Roads', 'planetaryTracks': 'Planetary Tracks', 'victoryPoints': 'Card VP', 'total': 'Total VP'};
        categories.forEach((cat, index) => {
          const tmp: {gen: string, value: Number}[] = [];
          for (const [k, v] of Object.entries(hist)) {
            // @ts-ignore
            tmp.push({gen: k, value: v[cat]});
          }
          tmp.sort((a, b) => (parseInt(a.gen) > parseInt(b.gen)) ? 1 : -1);
          tmp.forEach((g) => {
            playerData[index]['data'].push(g.value);
          });

          chartData[index].data.datasets.push(playerData[index]);
          // @ts-ignore
          chartData[index].options.scales.yAxes.title.text = categoryLabels[cat];
          // @ts-ignore
          chartData[index].options.plugins.title.text = categoryLabels[cat];
        });
      });
      // @ts-ignore
      new Chart(document.getElementById('points-chart-VPTotal') as HTMLCanvasElement, chartData[11]);
      // @ts-ignore
      new Chart(document.getElementById('points-chart-VPCards') as HTMLCanvasElement, chartData[10]);
      // @ts-ignore
      new Chart(document.getElementById('points-chart-TR') as HTMLCanvasElement, chartData[0]);
      // @ts-ignore
      new Chart(document.getElementById('points-chart-Green') as HTMLCanvasElement, chartData[3]);
      // @ts-ignore
      new Chart(document.getElementById('points-chart-City') as HTMLCanvasElement, chartData[4]);
      // @ts-ignore
      new Chart(document.getElementById('points-chart-Milestone') as HTMLCanvasElement, chartData[1]);
      // @ts-ignore
      new Chart(document.getElementById('points-chart-Award') as HTMLCanvasElement, chartData[2]);
      // @ts-ignore
      new Chart(document.getElementById('points-chart-EV') as HTMLCanvasElement, chartData[5]);
      // @ts-ignore
      new Chart(document.getElementById('points-chart-MoonCol') as HTMLCanvasElement, chartData[6]);
      // @ts-ignore
      new Chart(document.getElementById('points-chart-MoonMine') as HTMLCanvasElement, chartData[7]);
      // @ts-ignore
      new Chart(document.getElementById('points-chart-MoonRoad') as HTMLCanvasElement, chartData[8]);
      // @ts-ignore
      new Chart(document.getElementById('points-chart-Planet') as HTMLCanvasElement, chartData[9]);
    },
  },
  mounted() {
    this.updateCharts();
  },
});


</script>
