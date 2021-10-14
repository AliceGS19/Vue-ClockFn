<template>
  <div id="container" v-if="clockFN === 'timer'">
    <ClockTimer />
    <div id="btn">
      <button  
        type="button" 
        class="btn btn-primary" 
        v-on:click.prevent="changeClockFunction" 
        id="fn-btn"
        v-if="clockFN === 'timer'"
        >
        Cronômetro
      </button>
    </div>
  </div>
  <div id="container" v-if="clockFN === 'cronometer'">
    <ClockCronometer />
    <div id="btn">
      <button  
        type="button" 
        class="btn btn-primary" 
        v-on:click.prevent="changeClockFunction" 
        id="fn-btn"
        v-if="clockFN === 'cronometer'"
        >
        Timer
      </button>
    </div>
  </div>  
</template>

<script>
import ClockTimer from './components/ClockTimer.vue'
import ClockCronometer from './components/ClockCronometer.vue'

export default {
  name: 'App',
  components: {
    ClockTimer,
    ClockCronometer
  },
  data() {
    return {
      clockFN: 'timer'
    }
  },
  methods: {
    changeClockFunction() {
      switch (this.clockFN) {
        case 'timer':
        this.clockFN = 'cronometer'
        break;

        case 'cronometer':
        this.clockFN = 'timer';
        break;
      }
    }
  },
}
</script>

<style>
#app {
  background-color:black;
  min-width: 900px;
  min-height: 1440px;
}
#container {
  padding-top: 10%;
  margin-bottom: 20%;
  margin-right: 30%;
  margin-left: 30%
}

#btn {
  display: flex;
  justify-content: center;
  margin-top: 40px;
}
#fn-btn {
    background-color: green;
    color: black;
}
</style>
