<script setup>

</script>

<template>
    <section id="welcome">
        <div class="benefits">
            <h2>Complete this program<br/>if you want...</h2>
            <div>
                <p>✅ Follow a simple program with proven results.</p>
                <p>✅ Get fit, healthy, strong and absolutely shredded.</p>
                <p>✅ Learn more about gym, training and technique.</p>
            </div>
        </div>
        <div>
            <h3>The Training Plan</h3>
            <p>This training plan follows a structure known as the
                <strong>Bro Split</strong>
                <h5><i>Push &rarr; Pull &rarr; Legs &rarr; Repeat</i></h5>
            </p>
        </div>
        <div class="card challenge">
            <h3>🔥 Your challenge</h3>
            <p>Complete all the workout and track your progress along the way!</p>
            <p>Do you accept?</p>
            <button>Begin &rarr;</button>
        </div>
    </section>
</template>

<style scoped>
    #welcome,
    .challenge,
    .benefits {
        display: flex;
        flex-direction: column;
    }

    #welcome {
        gap: 1.5rem;
    }

    .benefits {
        gap: 0.5rem;
    }


</style>
