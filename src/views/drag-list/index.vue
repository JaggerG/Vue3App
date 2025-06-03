<template>
    <div class="drag-list-container">
        <h1>DragList</h1>
        <DragList>
            <template #drag>
                <div id="drag-box">
                    <div class="drag-item" v-for="item in 9" :key="item" :data-index="item">{{ item }}</div>
                </div>
            </template>
        </DragList>

    </div>
</template>
<script setup lang="ts">
import { onMounted } from 'vue';
import DragList from '@/components/DragList.vue';
onMounted(() => {
    console.log('drag-list mounted');
})
</script>
<style scoped lang="scss">
.drag-list-container {
    width: 100%;
    height: 100%;
    background-color: #f5f5f5;

    .drag-item {
        width: 100px;
        height: 40px;
        background-color: aquamarine;
        margin: 5px;
    }
}
</style>
