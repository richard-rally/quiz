<template>
    <ul class="mb-5">
        <h4 class="mb-3">{{ round.title }}</h4>

        <div v-if="revealAll">
            <Question :question-number="index" :question="question" :key="index" v-for="(question, index) in round.questions"></Question>
        </div>

        <div v-else>

            <Question :question-number="questionIndex" :question="selectedQuestion"></Question>
            <button @click="questionIndex--" :disabled="questionIndex === 0">Previous question</button>
            <button @click="questionIndex++" :disabled="questionIndex === length - 1">Next question</button>

            <p class="text-center"> Question {{ questionIndex + 1}} of {{ length }} </p>
        </div>

        <button @click="revealAll = ! revealAll">Reveal All</button>
    </ul>
</template>

<script>

    import Question from "@/components/Question";

    export default {
        name: "QuestionGroup",

        components: {
            Question
        },

        props:{
            round: Object
        },

        data () {
            return {
                questionIndex: 0,
                revealAll: false
            }
        },

        computed: {
            length () {
                return this.round.questions.length;
            },

            selectedQuestion () {
                return this.round.questions[this.questionIndex];
            }
        },

        watch: {
            round: {
                deep: true,
                handler () {
                    this.questionIndex = 0;
                }
            }
        },

        methods: {

        }
    }
</script>

<style scoped>

</style>