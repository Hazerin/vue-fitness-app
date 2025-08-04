<script setup>
    import { workoutProgram } from '../../utils';
    const selectedWorkout = 4
    const {workout, warmup} = workoutProgram[selectedWorkout]
</script>

<template>
    <section id="workout-card">
        <div class="plan-card-header">
            <div class="plan-card-header">
                <p>Day {{ selectedWorkout < 9 ? '0' + selectedWorkout : selectedWorkout }}</p>

            </div>
        </div>
    </section>
</template>

<style scoped>

</style>