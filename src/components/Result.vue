<script setup>
import { defineProps, computed } from 'vue';
const props = defineProps(['results', 'totalCorrect', 'questionLength'])

let resultIndex = computed(() => {
    let index = 0;
    props.results.forEach((e, i) => {
        if (e.min <= props.totalCorrect && e.max >= props.totalCorrect) {
            index = i
        }
    });
    return index;
})

const resultStatus = computed(() => {
    return `${props.totalCorrect} asnwer are correct from ${props.questionLength} Questions`
})

</script>

<template>
    <div class="result">
        <div class="title">{{ results[resultIndex].title }} </div>
        <div class="desc">
            {{ results[resultIndex].desc }}
            <span>Result: {{ resultStatus }}</span>
        </div>
    </div>
</template>

<style scoped ></style>