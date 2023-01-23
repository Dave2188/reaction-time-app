<template>
	<Block :style="cssVars" class="block" v-if="isPlaying" :delay="delay" @end="endGame" />

	<div class="titleBlock">
		<h1>Reaction time app</h1>
		<button @click="start" :disabled="isPlaying">Play</button>
		<Results v-if="showResults" :score="score" />
	</div>

</template>

<script>
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";

export default {
	name: "app",
	components: { Block, Results },
	data() {
		return {
			isPlaying: false,
			delay: null,
			score: null,
			showResults: false,
			xPosition: null,
			yPosition: null,
		};
	},
	methods: {
		start() {
			this.delay = 2000 + Math.floor(Math.random() * 5000);
			this.isPlaying = true;
			this.showResults = false;
			this.randomPosition();
		},
		endGame(reactionTime) {
			this.score = reactionTime;
			this.isPlaying = false;
			this.showResults = true;
		},
		randomPosition() {
			this.yPosition = Math.floor(Math.random() * (window.screen.availHeight - 64)) + "px";
			this.xPosition = Math.floor(Math.random() * (window.screen.availWidth - 104)) + "px";
			if (this.yPosition < 0) this.xPosition += 64;
			if (this.xPosition < 0) this.xPosition += 104;
		},
	},
	computed: {
		cssVars() {
			return {
				top: this.yPosition,
				left: this.xPosition,
			};
		},
	},
};
</script>

<style>
#app {
	align-items: center;
	display: flex;
	flex-direction: column;
	height: 100vh;
	justify-content: center;
	margin: 0;
	padding: 0;
	text-align: center;
	width: 100vw;
}


#app button {
	color: black;
	background-color: rgb(1, 252, 168);

}

#app button:hover {
	box-shadow: 2px 2px 10px white;
	border: 2px solid black;
}

#app .block {
	position: absolute;
	margin: 0;
}

button:disabled {
	cursor: not-allowed;
	opacity: 0.3;
}
</style>

