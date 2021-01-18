<template>
  <div id="app">
    <div class="wrapper">
      <h1>Strategy Marketplace</h1>
      <div class="filters">
        <span class="filters-btn-main">Filters</span>
        <div class="filters-buttons">
          <button class="filters-btn active" @click="applyFilter('all')">All</button>
          <button class="filters-btn" @click="applyFilter('basket')">Basket</button>
          <button class="filters-btn" @click="applyFilter('bots')">Bots</button>
          <button class="filters-btn" @click="applyFilter('coming soon')">Coming soon</button>
        </div>
      </div>
      <div>
        <transition-group name="fade" class="cards-wrapper">
          <Card v-for="(card, index) in filtredList" :card="card" :key="index"></Card>
        </transition-group>
      </div>
    </div>
  </div>
</template>

<script>
import Card from './components/Card.vue'

export default {
  name: 'App',
  components: {
    Card
  },
  data() {
    return {
      filterValue: 'all',
      cards: [
        {
          filter: "bots",
          type: "doughnut",
          cardTitle: "BG 6 Basket",
          chartData: {
            labels: ['Bitcoin', 'Litecoin', 'Ethereum', 'Ripple', 'Stellar'],
            datasets: [{
                hoverBorderWidth: 2,
                borderColor: '#fff',
                data: [3, 10, 5, 2],
                backgroundColor: [
                    '#627eea',
                    '#f7931a',
                    '#26a17b',
                    '#8dc351',
                    '#e0dfdf',
                    '#3b536c',
                ]
            }]
          }

        },
        {
          filter: "basket",
          type: "doughnut",
          cardTitle: "BG 8 Index",
          chartData: {
            labels: ['Bitcoin', 'Litecoin', 'Ethereum', 'Ripple', 'Stellar'],
            datasets: [{
                borderColor: '#fff',
                hoverBorderWidth: 2,
                data: [7, 13, 3, 2,],
                backgroundColor: [
                    '#627eea',
                    '#f7931a',
                    '#26a17b',
                    '#8dc351',
                    '#e0dfdf',
                    '#3b536c',
                ]
            }]
          }
          
        }
      ],
    }
  },
  computed: {
    filtredList: function(){
      let val = this.filterValue;
      return this.cards.filter(function(elem){
        if(val == "all"){
          return elem;
        } else if(val == elem.filter) {
          return elem;
        } else {
          return false
        }
      })
    }
  },
  methods: {
    applyFilter(val){
      this.filterValue = val;
      let btns = document.querySelectorAll('.filters-btn');
      btns.forEach(el=> {
        el.classList.remove('active')
      });
      event.target.classList.add('active');
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  padding: 0;
  margin: 0;
}
.wrapper {
  width: 1000px;
  margin: 0 auto;
  padding: 30px 50px;
  height: 100%;
  min-height: 100vh;
  background: linear-gradient(to bottom, #fafbfd 0%,#eff1f7 100%);
}
h1 {
  text-align: left;
  color: #3c3463;
}
.filters {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  margin-bottom: 30px;
}
.filters-btn-main {
  font-size: 14px;
  display: flex;
  align-items: center;
  height: 30px;
  padding: 0 15px;
  color: #959cbd;
  border: 1px solid #959cbd;
  border-radius: 4px;
  background-color: transparent;
}
.filters .filters-buttons {
  margin-left: 30px;
}
.filters .filters-buttons *:not(:last-child){
  margin-right: 5px;
}
.filters .filters-buttons button {
  height: 30px;
  padding: 0 15px;
  border: none;
  border-radius: 4px;
  font-size: 12px;
  color: #959cbd;
  background-color: transparent;
  cursor: pointer;
}
.filters .filters-buttons button:focus {
  border: none;
  outline: none;
}
.filters .filters-buttons button.active {
  background-color: #4a4ae2;
  color: #fff;
}
.cards-wrapper {
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

</style>
