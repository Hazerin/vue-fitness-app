<script setup>
    import { workoutProgram } from '../utils';
    const workoutTypes = ['Push','Pull','Legs'];

</script>

<template>
    <section id="grid">
        <!--Coppia chiave-valore (0 : "0", 1 : "1" etc) in modo da dare a ogni pulsante una chiave unica per l'identificazione-->
        <button :key="workoutIdx" v-for="(workout, workoutIdx) in Object.keys(workoutProgram)" class="card-button plan-card" >
            <div>
                <p>Day {{ workoutIdx < 9 ? "0" + (workoutIdx + 1) : workoutIdx + 1}}</p>
                <i class="fa-solid fa-dumbbell"></i>
                <i class="fa-solid fa-weight-hanging"></i>
                <i class="fa-solid fa-bolt"></i>
            </div>
            <h3>ITEMS</h3>
        </button>
    </section>
</template>

<style scoped>

</style>
