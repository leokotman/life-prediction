<template>
    <div>
        <predict-header />
        prediction quiz form
        <div v-if="isLoading">loading spinner</div>
        <div v-if="isRecording">Запись сообщения</div>
        <span>вопрос № - 5</span>
    </div>
</template>

<script>
import PredictHeader from "./PredictHeader.vue";

    export default {
        components: {
            PredictHeader,
        },
        data() {
            return{
                isLoading: true,
                isRecording: false,
            }
        }
    }
</script>

<style scoped>

</style>