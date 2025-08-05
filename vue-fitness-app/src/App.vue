<script setup>
    import Welcome from './components/pages/Welcome.vue'
    import Layout from './components/layouts/Layout.vue'
    import Dashboard from './components/pages/Dashboard.vue'
    import Workout from './components/pages/Workout.vue'

    import { ref, computed, onMounted } from 'vue'
    import { workoutProgram } from './utils'

    const defaultData = {}
        for (let workoutIdx in workoutProgram) {
        const workoutData = workoutProgram[workoutIdx]

        defaultData[workoutIdx] = {} 

        for (let e of workoutData.workout) {
            defaultData[workoutIdx][e.name] = ''
        }
    }

    const selectedDisplay = ref(1)
    const data = ref(defaultData)
    const selectedWorkout = ref(-1)

    const isWorkoutComplete = computed(() => {
    const currWorkout = data.value?.[selectedWorkout.value]
        if (!currWorkout) { return false }

        // Ogni esercizio del workout corrente deve essere completato (!!ex è doppia negazione, quindi vero)
        // La doppia negazione è necessaria per non fare ritornare l'esercizio ma piuttosto se questo risulta completato.
        const isCompleteCheck = Object.values(currWorkout).every(ex => !!ex)
        console.log('ISCOMPLETE: ', isCompleteCheck)
        return isCompleteCheck
    })

    const firstIncompleteWorkoutIndex = computed(() => {
    const allWorkouts = data.value
        if (!allWorkouts) { return -1 }

        // Ciclo su ogni coppia chiave valore e verifica se il workout è completato o no
        for (const [index, workout] of Object.entries(allWorkouts)) {
        const isComplete = Object.values(workout).every(ex => !!ex)
            if (!isComplete) {
                return parseInt(index)
            }
        }
        // Tutti gli esercizi sono stati completati
        return -1 
    })

    function handleChangeDisplay(idx) {
        selectedDisplay.value = idx
    }

    function handleSelectWorkout(idx) {
        selectedDisplay.value = 3
        selectedWorkout.value = idx
    }

    function handleSaveWorkout() {
        // salva i dati nel localstorage del browser
        localStorage.setItem('workouts', JSON.stringify(data.value))
        // mostra la dashboard
        selectedDisplay.value = 2
        // Deseleziona un workout
        selectedWorkout.value = -1
    }

    function handleResetPlan() {
        selectedDisplay.value = 1
        selectedWorkout.value = -1
        data.value = defaultData
        localStorage.removeItem('workouts')
        location.reload()
    }

    // Quando l'applicazione viene caricata
    onMounted(() => {
        // Non fare niente se localStorage è vuota
        if (!localStorage) {return}
        // Se ci sono degli allenamenti, recupero i dati
        if (localStorage.getItem('workouts')) {
            const savedData = JSON.parse(localStorage.getItem('workouts'))
            data.value = savedData
            // Se ci sono dati, non è necessario caricare la pagina di benvenuto e passo direttamente a quella degli allenamenti
            selectedDisplay.value = 2
        }
    })

</script>

<template>
    <Layout>
        <!-- Nell'HTML di Vue viene sottointeso il value direttamente. Quindi selectedDisplay equivale a selectedDisplay.value -->
        <Welcome :handleChangeDisplay="handleChangeDisplay" v-if="selectedDisplay == 1" />
        <Dashboard :handleResetPlan="handleResetPlan" :firstIncompleteWorkoutIndex="firstIncompleteWorkoutIndex" :handleSelectWorkout="handleSelectWorkout" v-if="selectedDisplay == 2"/>
        <Workout :handleSaveWorkout="handleSaveWorkout" :isWorkoutComplete="isWorkoutComplete" :data="data" :selectedWorkout="selectedWorkout" v-if="workoutProgram?.[selectedWorkout]"/>
    </Layout>
</template>

<style scoped>

</style>
