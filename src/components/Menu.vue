<template>
	<div
		class='menu'
		:class='{menuOpen}'
	>
		<div
			class='hamburger'
			@click='menuOpen = !menuOpen'
		>
			<div class='top'></div>
			<div class='bottom'></div>
		</div>
		<div class='menuList'>
			<div
				title='Home'
				@click='$emit("reset")'
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					viewBox="0 0 576 512"
				>
					<path
						fill="currentColor"
						d="M280.37 148.26L96 300.11V464a16 16 0 0 0 16 16l112.06-.29a16 16 0 0 0 15.92-16V368a16 16 0 0 1 16-16h64a16 16 0 0 1 16 16v95.64a16 16 0 0 0 16 16.05L464 480a16 16 0 0 0 16-16V300L295.67 148.26a12.19 12.19 0 0 0-15.3 0zM571.6 251.47L488 182.56V44.05a12 12 0 0 0-12-12h-56a12 12 0 0 0-12 12v72.61L318.47 43a48 48 0 0 0-61 0L4.34 251.47a12 12 0 0 0-1.6 16.9l25.5 31A12 12 0 0 0 45.15 301l235.22-193.74a12.19 12.19 0 0 1 15.3 0L530.9 301a12 12 0 0 0 16.9-1.6l25.5-31a12 12 0 0 0-1.7-16.93z"
					/></svg>
				<span class='menuTitle'>Home</span>
			</div>

			<div
				class='theme'
				@click='$emit("change-theme")'
				title='Change Theme'
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					aria-hidden="true"
					focusable="false"
					data-prefix="fas"
					data-icon="adjust"
					class="svg-inline--fa fa-adjust fa-w-16"
					role="img"
					viewBox="0 0 512 512"
				>
					<path
						fill="currentColor"
						d="M8 256c0 136.966 111.033 248 248 248s248-111.034 248-248S392.966 8 256 8 8 119.033 8 256zm248 184V72c101.705 0 184 82.311 184 184 0 101.705-82.311 184-184 184z"
					/></svg>
				<span class='menuTitle'>Theme</span>
			</div>

			<div
				title='Show / Hide Guides'
				@click='$emit("toggle-details")'
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					viewBox="0 0 576 512"
				>
					<path
						fill="currentColor"
						d="M572.52 241.4C518.29 135.59 410.93 64 288 64S57.68 135.64 3.48 241.41a32.35 32.35 0 0 0 0 29.19C57.71 376.41 165.07 448 288 448s230.32-71.64 284.52-177.41a32.35 32.35 0 0 0 0-29.19zM288 400a144 144 0 1 1 144-144 143.93 143.93 0 0 1-144 144zm0-240a95.31 95.31 0 0 0-25.31 3.79 47.85 47.85 0 0 1-66.9 66.9A95.78 95.78 0 1 0 288 160z"
					/></svg>
				<span class='menuTitle'>View</span>
			</div>
			<div
				@click='printSudoku'
				title='Print Sudoku and Solution'
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					viewBox="0 0 512 512"
				>
					<path
						fill="currentColor"
						d="M448 192V77.25c0-8.49-3.37-16.62-9.37-22.63L393.37 9.37c-6-6-14.14-9.37-22.63-9.37H96C78.33 0 64 14.33 64 32v160c-35.35 0-64 28.65-64 64v112c0 8.84 7.16 16 16 16h48v96c0 17.67 14.33 32 32 32h320c17.67 0 32-14.33 32-32v-96h48c8.84 0 16-7.16 16-16V256c0-35.35-28.65-64-64-64zm-64 256H128v-96h256v96zm0-224H128V64h192v48c0 8.84 7.16 16 16 16h48v96zm48 72c-13.25 0-24-10.75-24-24 0-13.26 10.75-24 24-24s24 10.74 24 24c0 13.25-10.75 24-24 24z"
					/></svg>
				<span class='menuTitle'>Print</span>
			</div>
		</div>

	</div>
</template>

<script>
export default {
	data() {
		return {
			menuOpen: false,
			darkMode: false,
		};
	},

	methods: {
		printSudoku() {
			window.print();
		},
	},
};
</script>

<style >
.menu {
	position: fixed;
	left: 1em;
	top: 1em;
	/* width: 3em; */
	overflow: hidden;
}

.menuList {
	/* height: 15em; */
	margin-top: 3em;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	transform: translateY(-150%);
	transition: 0.5s cubic-bezier(0.445, 0.05, 0.55, 0.95);
}

.menuList div {
	display: flex;
	flex-direction: column;
	align-items: center;
	margin-bottom: 0.5em;
}

.menuOpen .menuList {
	transform: translateX(0);
}

.hamburger {
	position: absolute;
	z-index: 5;
	height: 2em;
	width: 2em;
}

.hamburger div {
	height: 0.25em;
	width: 2em;
	background: currentColor;
	border-radius: 15px;
	margin: 0.5em;
	transition: transform 0.5s cubic-bezier(0.075, 0.82, 0.165, 1);
	/* transform-origin: top center; */
}

.menuOpen .hamburger .top {
	transform: rotate(45deg) translateY(0.5em);
}
.menuOpen .hamburger .bottom {
	transform: rotate(-45deg) translateY(-0.5em);
}

.menu svg {
	height: 2em;
	width: 2em;
}

/* Themes */

/* .day .dark {
	background: deepskyblue;
	color: white;
}

.day .light {
	background: lightskyblue;
	color: black;
} */
</style>