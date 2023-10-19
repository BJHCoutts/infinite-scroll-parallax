<script>
	import PuzzlePieces from "../lib/assets/PuzzlePieces.svelte";

</script>

<main class="scroll-container">
	
	<h1>Scroll Down!</h1>

	<!-- <PuzzlePieces /> -->

</main>

<style>

	.scroll-container {
		/* height: 100vh;
		height: 100dvh;
		height: 100svh;
		height: 100lvh; */
		position: fixed;
		inset: 0;
		overflow: hidden scroll;
		perspective: 10px;
		background-image: url("$lib/assets/puzzlePieces.webp");
		background-position: 50% 75%;
	}

	h1 {
		position: relative;
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100%;
		transform-style: preserve-3d;
		z-index: -1
	}

</style>