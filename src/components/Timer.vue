<template>
	<div class='timer'>{{minutes}}:{{seconds}}</div>
</template>

<script>
let timeInterval;

export default {
	data() {
		return {
			minutes: null,
			seconds: null,
		};
	},

	props: {
		startMin: Number,
		startSec: Number,
	},

	methods: {
		tick() {
			if (this.seconds === null) {
				this.minutes = this.startMin;
				this.seconds = this.startSec;
			}
			this.seconds++;
			if (this.seconds >= 60) {
				this.minutes++;
				this.seconds = 0;
			}
		},
	},

	mounted() {
		timeInterval = setInterval(this.tick, 1000);
	},

	beforeDestroy() {
		clearInterval(timeInterval);
	},
};
</script>

<style>
.timer {
	width: 3em;
}
</style>