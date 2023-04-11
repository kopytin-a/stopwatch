<template>
    <stopwatch-item 
        v-for="totalTime in totalTimes" 
        :key="totalTime.id"
        :totalTime="totalTime"
        @remove="$emit('remove', totalTime)"
        @start="$emit('start', totalTime)"
        @stop="$emit('stop', totalTime)"
        @reset="$emit('reset', totalTime)"
    />
</template>

<script>
import StopwatchItem from '@/components/StopwatchItem.vue'
export default {
  components: { StopwatchItem },
    props: {
        totalTimes: {
            type: Array,
            required: true
        }
    }
}
</script>

<style scoped>

</style>