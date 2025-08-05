<script setup>
    import Layout from './components/layouts/Layout.vue';
    import Welcome from './components/pages/Welcome.vue';
    import Dashboard from './components/pages/Dashboard.vue';
    import Workout from './components/pages/Workout.vue';
    import {ref} from "vue"
    import { workoutProgram } from './utils';

    const defaultData = {};
    for (let workoutIdx in workoutProgram) {

        const workoutData = workoutProgram[workoutIdx]

        defaultData[workoutIdx] = {}

        for (let e of workoutData.workout) {
            defaultData[workoutIdx][e.name] = ''
        }

    }

    console.log(defaultData)


    const selectedDisplay = ref(3)
    const data = ref(defaultData)
    const selectedWorkout = ref(2)

</script>

<template>
    <Layout>
        <!-- Nell'HTML di Vue viene sottointeso il value direttamente. Quindi selectedDisplay equivale a selectedDisplay.value -->
        <Welcome v-if="selectedDisplay == 1"/>
        <Dashboard v-if="selectedDisplay == 2"/>
        <Workout :data="data" :selectedWorkout="selectedWorkout" v-if="workoutProgram?.[selectedWorkout]"/>
    </Layout>
</template>

<style scoped>

</style>
