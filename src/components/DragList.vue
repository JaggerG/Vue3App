<template>
    <div class="drag-list-container">
        <slot name="drag"></slot>
    </div>
</template>
<script setup lang="ts">
import { defineProps, onMounted } from "vue";
const props = defineProps({
    borderStyle: {
        type: String,
        default: '1px dashed red'
    }
})
onMounted(() => {
    const dragBoxObj = document.getElementById('drag-box')
    const dragItemList = dragBoxObj?.children as HTMLCollectionOf<HTMLElement>;
    let curDragObj: HTMLElement, enterDragObj: HTMLElement;
    let curDragIndex: any, enterDragIndex: any;
    for (let i = 0; i < dragItemList.length; i++) {
        dragItemList[i].draggable = true;
    }
    dragBoxObj?.addEventListener('dragstart', (event: DragEvent) => {
        const target = event.target as HTMLElement;
        curDragObj = target
        curDragIndex = target.dataset.index;
        curDragObj.style.opacity = '0.5';
    }, false)
    dragBoxObj?.addEventListener('dragenter', (event) => {
        const target = event.target as HTMLElement;
        console.log(target);
        enterDragObj = target;
        enterDragIndex = target.dataset.index;
        if (target.className === 'drag-item') {
            target.style.border = props.borderStyle;
        }
    }, false)
    dragBoxObj?.addEventListener('dragleave', (event) => {
        const target = event.target as HTMLElement;
        if (target.className === 'drag-item') {
            target.style.border = '';
        }
    })
    dragBoxObj?.addEventListener('drop', (event) => {
        event.preventDefault();
        if (curDragIndex !== enterDragIndex) {
            if (curDragIndex < enterDragIndex) {
                curDragObj.remove();
                enterDragObj.after(curDragObj);
            } else {
                curDragObj.remove();
                enterDragObj.before(curDragObj);
            }
        }
        for (let i = 0; i < dragItemList.length; i++) {
            dragItemList[i].dataset.index = i.toString();
            dragItemList[i].style.border = '';
        }
        curDragObj.style.opacity = '1';
    })
    dragBoxObj?.addEventListener('drag', (event) => {
    }, false)
    dragBoxObj?.addEventListener('dragexit', (event) => {
        event.preventDefault();
    })
    dragBoxObj?.addEventListener('dragover', (event) => {
        event.preventDefault();
    }, false)
})
</script>
<style scoped lang="scss">
.drag-list-container {

    #drag-box {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
    }

    .drag-item {
        user-select: none;
    }

    .enter {
        background-color: red;
        border: 1px dashed red;
    }

}
</style>
