<script lang='ts'>
	import { onMount } from "svelte";

	onMount(()=>{
		const scrollContainer = document.querySelector('.scroll-container')
		const header = document.querySelector('h1')

		function createEl() {

		}

		const observer:IntersectionObserver = new IntersectionObserver( (entries:IntersectionObserverEntry[]) => {
			
			if (entries[0].isIntersecting) {

				if (!scrollContainer) {console.error('scroll container is missing')}
				
				const newEl = document.createElement('h1')
				newEl.innerText = "Scroll Down!"
				
			}
		})

		if (header) {
			observer.observe(header)

		}

	})



</script>

<main class="scroll-container">
	
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
	<h1>Scroll Down!</h1>
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
		z-index: -1;
		/* display: none; */
	}

</style>