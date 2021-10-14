<template>
  <div id="counters">
    <h1>{{hours}} : {{minutes}} : {{seconds}}</h1>
  </div>  
      <div id="btn">
        <button 
          type="button" 
          class="btn btn-primary" 
          v-on:click.prevent="cronometer"
          id="fn-btn" 
          v-if="status === 'stopped'" 
          >
          Iniciar
        </button>
        <button 
          type="button" 
          class="btn btn-primary"
          v-on:click.prevent="cronometer"
          id="fn-btn" 
          v-if="status === 'started'"
          >
          Parar
        </button>
      </div>
</template>

<script>
export default {
  data() {
    return {
      hours: 0,
      minutes: 0,
      seconds: 0,
      status: "stopped",
    }
  },
  methods: {
    cronometer() {
      const interval = () => {
         setTimeout(() => {
          if (this.status === "started") {
            switch (this.seconds) {
            case 59:
            switch (this.minutes) {
              case 59:
              this.hours = this.hours + 1
              this.minutes = 0
                interval()
              break;

              default:
              this.minutes = this.minutes + 1
              interval()
            }
            this.seconds = 0
            break;
            
            default:
            this.seconds = this.seconds + 1
            interval()
          }
          }
        }, 1000)
      }
      const startTimer = () => {
        interval()
        this.status = "started"
    }
    const stopTimer = () => {
      this.status = "stopped";
      this.hours = 0;
      this.minutes = 0;
      this.seconds = 0;
    }
    if(this.status === "stopped") {
      startTimer();
    } else {
      stopTimer();
    }
  }
  }
}
</script>


<style>
#counters {
  display:flex;
  justify-content: center;
}

#form-label {
    color: green;
}

#btn {
   display: flex;
   justify-content: center; 
}

#fn-btn {
    background-color: green;
    color: black;
}
</style>