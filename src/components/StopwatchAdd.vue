<template>
    <div class="block__block">
        <div class="block__stopwatch">
            <my-button 
                class="block__addStopwatch" 
                @click="addStopwatch"
            >
                <img src="@/assets/addStopwatch.png">
            </my-button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            newId: 2
        }
    },
    methods: {
        addStopwatch() {
            const newStopwatch = {
                id: this.newId++,
                millisecond: 0,
                seconds: '00',
                minutes: 0,
                hours: 0,
                timerId: '',
                stopTime: 0,
                timeStart: null,
                startAndStop: false,
                blockMinutes: false,
                blockHours: false
            }

            this.$emit('create', newStopwatch)
        }
    }
}
</script>

<style scoped>
    .block__block{
        padding-right: 50px;
        padding-bottom: 45px;
    }

    .block__addStopwatch{
        background: none;
        display: block;
        margin: auto;
        padding-top: 50px;
    }

    .block__stopwatch{
        min-width: 225px;
        min-height: 120px;
        background-color: #696969;
    }
</style>