<script>
import { Doughnut } from 'vue-chartjs';

export default {
  extends: Doughnut,
  props: ['chartdata'],
  methods: {
    handleHover(event, elem){
      let item = elem[0];
      if(item){
        this.$emit('onHoverData', {
          type: event.type,
          index: item._index,
          backgroundColor: item._view.backgroundColor,
          value: this.chartdata.datasets[0].data[item._index]
        })
        this.$data._chart.update();
      } else {
        this.$emit('resetData');
      }
    }
  },
  mounted () {
    this.renderChart(this.chartdata, {
      cutoutPercentage: 90,
      legend: {
        display: false,
        onClick: this.legendClick
      },
      animation: {
        animateScale: true
      },
      tooltips: {
        enabled: false,
      },
      events: ["mousemove"],
      onHover: this.handleHover
    });
  },

}
</script>

<style>
</style>