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

@media screen and (max-width: 550px) {
	.sudoku {
		/* display: block; */
		/* position: absolute; */
		justify-content: flex-start;
		margin-top: 4em;
		/* left: 0; */
		/* top: 4em; */
		/* right: 0; */
		height: 90vh;
	}

	.grid,
	.digits button {
		font-size: 5vw;
	}
	.digits {
		justify-content: center;
		margin-top: 0.5em;
	}

	.cell {
		height: 2em;
		width: 2em;
	}

	.menu {
		/* top: 0.25em;
		left: 0.25em; */
		width: 90vw;
	}

	.menuTitle {
		display: none;
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
