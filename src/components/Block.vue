<template>
  <div class="block" v-if="showBlock" @click="stopTimer"><span>Click Me</span></div>
</template>

<script>
export default {
  props: ["delay"],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
    };
  },
  mounted() {
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay);
  },

  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10);
    },
    stopTimer() {
      clearInterval(this.timer);
      this.$emit("end", this.reactionTime);
    },
  },
};
</script>

<style scoped>
.block {
  width: 13rem;
  height: 8rem;
  border-radius: 1.5rem;
  background-color: blueviolet;
  color: white;
  text-align: center;
  padding: 8rem auto;
  margin: 3.2rem auto;
}

.block span {
  font-size: large;
  position: relative;
  top: 3.3rem;
}
</style>
