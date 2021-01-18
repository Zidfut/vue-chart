<script>
import { Doughnut } from 'vue-chartjs';

export default {
  extends: Doughnut,
  props: ['chartdata', 'showLegend'],
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
        
      } else {
        this.$emit('resetData');
      }
    },
    updateData(){
      this.$data._chart.update();
    },
    toggleChartData(index){
      let meta = this.$data._chart.getDatasetMeta(0);
      meta.data[index].hidden = !meta.data[index].hidden;
    }
  },
  mounted () {
    this.renderChart(this.chartdata, {
      cutoutPercentage: 88,
      legend: {
        display: false
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