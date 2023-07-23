<script setup>

import { defineProps, defineEmits, computed } from 'vue';

const props = defineProps(['questions', 'questionsAnswered'])
const emit = defineEmits(['questionAnswered'])

const barWidth = computed(() => {
    return {
        width: `${(props.questionsAnswered / props.questions.length) * 100}%`
    }
})

const barStatus = computed(() => {
    return `${props.questionsAnswered} out of ${props.questions.lenght} questions answered`
})

const selectAns = (answer) => {
    emit('questionAnswered', answer)
}


</script>

<template>
    <div class="questions-ctr">
        <div class="progress">
            <div class="bar" :style="barWidth"></div>
            <div class="status">{{ barStatus }}</div>
        </div>
        <transition-group name="fade">
            <div class="single-question" v-for="(question, index) in questions" :key="question.q"
                v-show="questionsAnswered === index">
                <div class="question">{{ question.q }}</div>
                <div class="answers">
                    <div class="answer" v-for="answer in question.answers" :key="answer.text"
                        @click.prevent="selectAns(answer.is_correct)">
                        {{ answer.text }}
                    </div>
                </div>
            </div>
        </transition-group>
    </div>
</template>

<style scoped ></style>