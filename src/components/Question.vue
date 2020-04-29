<template>
    <li class="mb-4">

        <div class="clearfix">
            <strong class="float-left mr-2">{{ questionNumber + 1 }}: </strong>
            <audio controls :src="question.audio" v-if="showAudio" class=" mb-3"></audio>
            <p v-else class="float-left"><strong>{{ question.title }}</strong></p>
            <button class="ml-3" @click="answerVisible = ! answerVisible">Reveal answer</button>
        </div>
        <em v-if="answerVisible === true" >A: {{ question.answer }}</em>
        <br>
    </li>
</template>

<script>
    export default {
        name: "Question",

        props: {
            question: Object,
            questionNumber: Number
        },

        computed: {
            showAudio () {
                return this.question.audio !== undefined;
            }
        },

        data () {
            return {
                answerVisible: false
            }
        },

        watch: {
            question: {
                deep: true,
                handler() {
                    this.answerVisible = false
                }
            }
        }
    }
</script>

<style scoped>

</style>