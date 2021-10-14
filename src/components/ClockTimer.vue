<template>
    <div id="counters">
      <h1>{{hours}} : {{minutes}} : {{seconds}}</h1>
    </div>  
    <form>
      <div class="form-group">
        <label for="hours" id="form-label">Horas</label>
        <input type="number" class="form-control" id="hours" v-model="hours">
        <label for="minutes" id="form-label">Minutos</label>
        <input type="number" class="form-control" id="minutes" v-model="minutes">
        <label for="seconds" id="form-label">Segundos</label>
        <input type="number" class="form-control" id="seconds" v-model="seconds">
      </div>
      <div id="btn">
        <button 
          type="button" 
          class="btn btn-primary" 
          v-on:click.prevent="timer"
          id="fn-btn" 
          v-if="status === 'stopped'" 
          >
          Iniciar
        </button>
        <button 
          type="button" 
          class="btn btn-primary"
          v-on:click.prevent="timer"
          id="fn-btn" 
          v-if="status === 'started'"
          >
          Parar
        </button>
      </div>
    </form>
</template>

<script>
export default {
  data() {
    return {
      hours: 0,
      minutes: 0,
      seconds: 0,
      status: "stopped",
      clockFN: 'timer'
    }
  },
  methods: {
    timer() {
      const interval = () => {
         setTimeout(() => {
          if (this.status === "started") {
            switch (this.seconds) {
            case 0:
            switch (this.minutes) {
              case 0:
              switch (this.hours) {
                case 0:
                this.status = "stopped"
                break;

                default:
                this.hours = this.hours - 1
                interval()
              }
              break;

              default:
              this.minutes = this.minutes - 1
              interval()
            }
            break;
            
            default:
            this.seconds = this.seconds - 1
            interval()
          }
          }
        }, 1000)
      }
      const startTimer = () => {
      const absoluteHours = Math.abs(Math.round(this.hours));
      const absoluteMinutes = Math.abs(Math.round(this.minutes));
      const absoluteSeconds = Math.abs(Math.round(this.seconds));
      if(absoluteHours !== 0 || absoluteMinutes !== 0 || absoluteSeconds !== 0) {
        interval();
        this.status = "started"
      }
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
  color: green
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