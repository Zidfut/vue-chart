<template>
  <div class="card">
    <h2 class="card-title">{{card.cardTitle}}</h2>
    <div class="chart">
      <transition name="fade">
        <span v-if="activeValue" class="chart-percent">{{activeValue}}<span>%</span></span>
      </transition>
      <chart ref="canvas" @onHoverData="setData" @resetData="resetData" :chartdata="card.chartData" :options="chartOptions"/>
    </div>
    <span class="period">Period PnL</span>
    <span class="percent">50%</span>
    <div class="custom-legends">
      <ul>
        <li v-for="(item, index) in legendArr" :key="index">
          {{item}}
          <span class="chart-legend" :class="{active:  activeIndex == index}" :title="card.chartData.labels[index]" :style="`background-color:${card.chartData.datasets[0].backgroundColor[index]}`"></span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Chart from './Chart.vue'

export default {
  name: 'Card',
  components: {
    Chart
  },
  props: ['card', 'chartOptions'],
  data() {
    return {
      activeIndex: null,
      activeValue: 0,
      activeColor: null
    }
  },
  computed: {
    legendArr(){
      return this.card.chartData.datasets[0].data;
    }
  },
  methods: {
    setData(val){
      this.activeValue = val.value;
      this.activeIndex = val.index;
      this.card.chartData.datasets[0].hoverBorderColor = val.backgroundColor;
    },
    resetData(){
      this.activeIndex = null;
      this.activeValue = 0;
    },
  }
}
</script>

<style scoped>
  .card {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-start;
    width: 260px;
    height: 360px;
    background-color: #fff;
    border-radius: 10px;
    box-shadow: 0 0 15px rgba(0,0,0, .1);
    transition: .3s;
    margin: 0 15px 15px;
  }
  .card:hover {
    box-shadow: 0 0 25px rgba(0,0,0, .3);
  }
  .card-title {
    color: #3c3463;
  }
  .chart {
    width: 50%;
    margin-bottom: 30px;
    position: relative;
  }
  .chart-percent {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 28px;
    font-weight: bold;
    color: #3c3463;
  }
  .chart-percent span {
    font-size: 16px;
  }
  .period {
    font-size: 14px;
    color: #959cbd;
  }
  .percent {
    font-size: 32px;
    color: #5daf61;
  }
  .custom-legends ul {
    padding: 0;
    list-style: none;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .custom-legends .chart-legend {
    display: block;
    height: 15px;
    width: 15px;
    margin: 0 5px;
    transition: transform .2s;
  }
  .custom-legends .chart-legend.active {
    transform: scale(1.5);
  }
</style>