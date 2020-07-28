<template>
	<div
		id="app"
		:class='{darkMode}'
	>
		<Menu
			v-if='start'
			@change-theme='darkMode = !darkMode'
			@toggle-details='showDetails = !showDetails'
			@reset='start = false'
		/>

		<Sudoku
			v-if='start'
			:diff='diff'
			:showDetails='showDetails'
			:currentGame='currentGame'
		/>
		<div
			v-else
			class='setup'
		>
			<h1>Sudoku</h1>
			<div class='difficulty'>
				<div>
					Difficulty
				</div>

				<input
					type='range'
					min='1'
					max='10'
					v-model.number='diff'
				/>

			</div>
			<button
				@click='currentGame = false; start=true'
				class='start'
			>New Game</button>
			<button
				class='continue'
				v-if='hasCurrentGame'
				@click='currentGame = true; start = true'
			>
				Continue
			</button>
		</div>
	</div>
</template>

<script>
import Sudoku from "./components/Sudoku.vue";
import Menu from "./components/Menu.vue";

export default {
	name: "App",
	data() {
		return {
			diff: 5,
			start: false,
			darkMode: false,
			showDetails: true,
			currentGame: false,
			hasCurrentGame: false,
		};
	},
	components: {
		Sudoku,
		Menu,
	},

	created() {
		if (localStorage.currentGame !== undefined) {
			this.hasCurrentGame = true;
		}
	},
};
</script>

<style>
@font-face {
	font-family: "Merriweather";
	src: url("./assets/fonts/Merriweather-Bold.ttf");
}
@font-face {
	font-family: "SpecialElite";
	src: url("./assets/fonts/SpecialElite-Regular.ttf");
}

body,
html {
	margin: 0;
}

#app,
.setup {
	display: flex;
	justify-content: center;
	align-items: center;
	font-family: "SpecialElite";
}

#app {
	height: 100vh;
	background: #f8f9fa;
	color: #23272b;
	transition: background 1s cubic-bezier(0.075, 0.82, 0.165, 1);
}

#app.darkMode {
	background: #23272b;
	color: #f8f9fa;
}

h1,
h2,
.slider {
	font-family: "Merriweather";
}

.setup {
	flex-direction: column;
}

button {
	font-size: 1.25em;
	color: #f8f9fa;
	background-color: #007bff;
	border-color: #007bff;
	cursor: pointer;
	border: 1px solid;
	border-color: transparent;
	border-radius: 5px;
	padding: 0.5em;
	margin: 0.5em;
}

button:hover {
	color: #f8f9fa;
	background-color: #0069d9;
	border-color: #0062cc;
}

button.continue {
	background: #6c757d;
}

button.continue:hover {
	background: #5a6268;
}

.bar {
	position: relative;
	height: 1.5em;
	width: 10em;
	border-radius: 20px;
	border: 2px solid currentColor;
	overflow: hidden;
	background: #f8f9fa;
}

.slider {
	position: absolute;
	z-index: 1;
	top: 0;
	left: -10em;
	height: 1.5em;
	width: 10em;
}

.fill {
	position: absolute;
	z-index: 2;
	height: 100%;
	width: 100%;

	transition: background 0.5s cubic-bezier(0.075, 0.82, 0.165, 1);
}

.fill.easy {
	background: #28a745;
}
.fill.medium {
	background: #34459c;
}
.fill.hard {
	background: #dc3545;
}

.knob {
	position: absolute;
	right: -0.5em;
	z-index: 3;
	background: #007bff;
	color: #f8f9fa;
	display: flex;
	justify-content: center;
	align-items: baseline;
	user-select: none;
	height: 1.5em;
	width: 1.5em;
	border-radius: 50%;
}

@media screen and (max-width: 550px) {
	.sudoku {
		font-size: 5vw;
		width: 100vw;
	}

	.digits {
		width: 100vw;
	}

	.digits button {
		font-size: 5vw;
		padding: 0.3em;
	}

	.cell {
		height: 2em;
		width: 2em;
	}

	.menuList {
		/* height: 15em; */
		margin-top: 0em;
		margin-left: 2em;
		flex-direction: row;
		align-items: center;
		justify-content: space-around;
		transform: translateX(-150%);
		transition: 0.5s cubic-bezier(0.445, 0.05, 0.55, 0.95);
	}

	.menuList div {
		margin-left: 1em;
	}

	.menuOpen .menuList {
		transform: translateX(0);
	}
}

@media print {
	.sudoku {
		display: block;
	}

	.cell {
		color: #1d2124 !important;
		background: #f8f9fa !important;
	}

	.header,
	.menu,
	.digits {
		display: none;
	}

	.solution {
		display: block;
	}
}
</style>
