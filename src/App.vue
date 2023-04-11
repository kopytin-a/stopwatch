<template>
    <div class="wrapper">
        <div>
            <div class="container">
                <div class="block__row">
                    <stopwatch-list 
                        :totalTimes="totalTimes"
                        @remove="removeStopwatch"
                        @start="startStopwatch"
                        @stop="stopStopwatch"
                        @reset="resetStopwatch"
                    />
                    <stopwatch-add @create="addStopwatch" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import StopwatchAdd from '@/components/StopwatchAdd.vue'
import StopwatchList from '@/components/StopwatchList.vue'
export default {
    components: {
        StopwatchAdd,
        StopwatchList
    },
    data() {
        return {
            totalTimes: [{
                id: 1, 
                millisecond: 0, 
                seconds: "00", 
                minutes: 0, 
                hours: 0, 
                timerId: '', 
                stopTime: 0, 
                timeStart: null, 
                startAndStop: false, 
                blockMinutes: false, 
                blockHours: false
            }]
        }
    },
    methods: {
        startStopwatch(totalTime){
            this.totalTimes.map(task => {
                if(task.id == totalTime.id) {
                    task.startAndStop = true
                    task.timeStart = Date.now()

                    task.timerId = setInterval(() => {
                        task.millisecond = Date.now() - task.timeStart + task.stopTime
                        task.seconds = Math.trunc(task.millisecond / 1000) % 60
                        if (task.seconds < 10) task.seconds = '0' + task.seconds

                        task.minutes = Math.trunc(task.millisecond / 1000 / 60) % 60
                        if (task.minutes < 10) task.minutes = '0' + task.minutes
                        if (task.minutes > 0) task.blockMinutes = true

                        task.hours = Math.trunc(task.millisecond / 1000 / 60 / 60) % 60
                        if (task.hours > 0)task.blockHours = true
                    }, 100)
                }
            })
        },
        stopStopwatch(totalTime) {
            this.totalTimes.map(task => {
                if(task.id == totalTime.id) {
                    task.startAndStop = false
                    clearInterval(task.timerId)
                    task.stopTime = task.millisecond
                }
            })
        },
        resetStopwatch(totalTime) {
            this.totalTimes.map(task => {
                if(task.id == totalTime.id) {
                    clearInterval(task.timerId)
                    task.startAndStop = false
                    task.seconds = "0" + 0
                    task.minutes = 0
                    task.hours = 0
                    task.stopTime = 0
                    task.blockMinutes = false
                    task.blockHours = false
                }
            })
        },
        addStopwatch(newStopwatch){
            this.totalTimes.push(newStopwatch)
        },
        removeStopwatch(totalTime) {
            if(this.totalTimes.length > 1) {
                this.totalTimes = this.totalTimes.filter(p => p.id !== totalTime.id)
            }
        }
    }
}
</script>

<style>
  .wrapper{
    min-height: 100%;
    overflow: hidden;
    display: flex;
    flex-direction: column;
  }

  .container{
    max-width: 880px;
    margin: 0px auto;
  }

  .block__row{
    padding-top: 72px;
    padding-left: 50px;
    display: flex;
    flex-wrap: wrap;
  }
</style>
