<!--
 * @Descripttion: 
 * @version: 1.0
 * @Author: xinyan
 * @Date: 2023-09-06 16:05:02
 * @LastEditors: xinyan
 * @LastEditTime: 2024-08-16 13:54:37
-->
<template>
    <div :style="style" ref="domRef">
        <slot name="slot-scope" :data="data"></slot>
    </div>
</template>
<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const emit = defineEmits(['onSizeChange']);

const props = defineProps({
    style: {
        type: Object,
        default: () => { }
    },
    data: {
        type: Object,
        default: () => { }
    },
    index: {
        type: Number,
        default: 0
    }
})

const domRef = ref(null);
const resizeObserver = null;


onMounted(() => {
    const domNode = domRef.value.children[0];
    emit("onSizeChange", props.index, domNode);
    const resizeObserver = new ResizeObserver(() => {
        emit("onSizeChange", props.index, domNode);
    });
    resizeObserver.observe(domNode);
})

onUnmounted(() => {
    if (resizeObserver) {
        resizeObserver?.unobserve(domRef.value.children[0]);
    }
})
</script>