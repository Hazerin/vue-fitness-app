<script setup>
    import Layout from './components/layouts/Layout.vue';
    import Welcome from './components/pages/Welcome.vue';
    import Dashboard from './components/pages/Dashboard.vue';
    import Workout from './components/pages/Workout.vue';

    const selectedDisplay = 3

</script>

<template>
    <Layout>
        <Welcome v-if="selectedDisplay == 1"/>
        <Dashboard v-if="selectedDisplay == 2"/>
        <Workout v-if="selectedDisplay == 3"/>
    </Layout>
</template>

<style scoped>

</style>
