<template>
    <div class="block__block">
        <div class="block__stopwatch">
            <div class="block__remove">
                <my-button 
                    class="block__buttonRemove" 
                    @click="$emit('remove', totalTime)"
                >
                    &#10006
                </my-button>
            </div>
            <div class="block__time">
                <div v-if="totalTime.blockHours">{{ totalTime.hours }}:</div>
                <div v-if="totalTime.blockMinutes">{{ totalTime.minutes }}:</div>
                <div>{{ totalTime.seconds }}</div>
            </div>
            <hr class="block__hr">
            <div class="block__button">
                <my-button 
                    class="block__resume" 
                    v-if="totalTime.startAndStop == false" 
                    @click="$emit('start', totalTime)"
                >
                    <img src="@/assets/resume.png">
                </my-button>

                <my-button 
                    class="block__stop" 
                    v-else-if="totalTime.startAndStop == true" 
                    @click="$emit('stop', totalTime)"
                >
                    <img src="@/assets/stop.png">
                </my-button>

                <my-button 
                    @click="$emit('reset', totalTime)"
                >
                    <img src="@/assets/reset.png">
                </my-button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        totalTime: Object,
        required: true
    }
}
</script>

<style scoped>
    .block__block {
        padding-right: 50px;
        padding-bottom: 45px;
    }

    .block__stopwatch {
        min-width: 225px;
        min-height: 120px;
        background-color: #696969;
    }

    .block__remove {
        text-align: end;
        padding: 1px 5px 0px 0px;
    }

    .block__buttonRemove {
        background: none;
        color: #9E9E9E;
        font-size: 17px;
    }

    .block__time {
        padding-bottom: 20px;
        color: #9E9E9E;
        font-size: 22px;
        font-family: 'gothampro';
        display: flex;
        justify-content: center;
    }

    .block__hr {
        background-color: #9E9E9E;
        height: 1px;
    }

    .block__button {
        display: flex;
        margin-top: 20px;
    }

    .block__stop {
        margin: 0px 55px 0px 70px;
    }

    .block__resume {
        margin: 0px 48px 0px 70px;
    }
</style>