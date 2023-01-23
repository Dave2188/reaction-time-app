
<template>

    <div class="scoreBox">
        <h2>It took you {{ score }}ms</h2>
        <p class="rank">{{ rank }}</p>
    </div>

</template>


<script>
export default {
    props: ["score"],
    data() {
        return {
            rank: null,
        };
    },
    mounted() {
        if (this.score < 250) {
            this.rank = "Faster than light";
        } else if (this.score < 400) {
            this.rank = "faster than a speeding bullet";
        } else {
            this.rank = "Need more practice....";
        }
    },
};
</script>

<style scoped>
.scoreBox {
    border: 2px solid white;
    padding: 2rem 3rem;
    border-radius: 1.5rem;
    margin-top: 4rem;
}

.rank {
    font-style: italic;
    font-size: large;
    margin-top: 2rem;
    color: chartreuse;
}
</style>
