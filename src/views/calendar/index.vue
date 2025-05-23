<template>
    <div class="container">
        <Calendar />
    </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import Calendar from '@/components/Calendar.vue';
export default defineComponent({
    name: 'CalendarPage',
    components: {
        Calendar
    }
})
</script>
<style scoped lang="scss"></style>