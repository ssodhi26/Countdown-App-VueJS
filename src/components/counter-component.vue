<template>
    <div v-if = "loaded">
      test
        <section class="text-3xl flex flex-col">
        <h3 v-if = "!expired">Hello from Counter component! Below is a countdown timer.</h3>
        <h3 v-else>Time has expired</h3>
        </section>
        <section class="flex text-6xl">
            <div class="days mr-2 relative">{{displayDays}}
                <div class="label text-sm absolute bottom-0">days</div>
            </div>
            <span class="leading-snug">:</span>
            <div class="hours mx-2 relative">{{displayHours}}
                <div class="label text-sm absolute bottom-0">hours</div>
            </div>
            <span class="leading-snug">:</span>
            <div class="minutes mx-2 relative">{{displayMinutes}}
                <div class="label text-sm absolute bottom-0">minutes</div>
            </div>
            <span class="leading-snug">:</span>
            <div class="seconds mx-2 relative">{{displaySeconds}}
                <div class="label text-sm absolute bottom-0">seconds</div>
            </div>
        </section>
    </div>
</template>

<script>
export default {
  name: 'CounterComponent',
  props: ['year', 'month', 'date', 'hour', 'minute', 'second', 'millisecond'],
  data: () => ({
    displayDays: 0,
    displayHours: 0,
    displayMinutes: 0,
    displaySeconds: 0,
    loaded: false,
    expired: false
  }),
  computed: {
    _seconds: () => 1000,
    _minutes () {
      return this._seconds * 60
    },
    _hours () {
      return this._minutes * 60
    },
    _days () {
      return this._hours * 24
    },
    end () {
      return new Date(
        this.year,
        this.month,
        this.date,
        this.hour,
        this.minute,
        this.second,
        this.millisecond
      )
    }
  },
  mounted () {
    this.showRemaining()
  },
  methods: {
    formatNum (num) {
      return num < 10 ? '0' + num : num
    },
    showRemaining () {
      const timer = setInterval(() => {
        const now = new Date()
        const distance = this.end.getTime() - now.getTime()

        if (distance < 0) {
          clearInterval(timer)
          this.expired = true
          this.loaded = true
          return
        }

        const days = Math.floor(distance / this._days)
        const hours = Math.floor((distance % this._days) / this._hours)
        const minutes = Math.floor((distance % this._hours) / this._minutes)
        const seconds = Math.floor((distance % this._minutes) / this._seconds)
        this.displayDays = this.formatNum(days)
        this.displayHours = this.formatNum(hours)
        this.displayMinutes = this.formatNum(minutes)
        this.displaySeconds = this.formatNum(seconds)
        this.loaded = true
      }, 1000)
    }
  }

}
</script>

<style scoped>
.days{
    width: 120px;
}
.hours{
    width: 120px;
}
.minutes{
    width: 120px;
}
.seconds{
    width: 120px;
}

.flex.text-6xl{
    display: flex;
    padding:80px;
    justify-content: center;
    font-size: 30px;
}

.text-3xl.flex{
    display: flex;
    justify-content: center;
    font-size: 20px;
}
</style>
