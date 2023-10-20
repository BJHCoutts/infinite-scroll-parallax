<script lang='ts'>
	import { onMount } from "svelte";

	let i = 1

	function handleLoad({currentTarget}: {currentTarget: HTMLElement}) {
		currentTarget.style.opacity = '100'
		currentTarget.style.border = '2px solid red'
	}

	onMount(()=>{
		const scrollContainer = document.querySelector('.scroll-container')
		const headers = document.querySelectorAll('h1')

		const observer:IntersectionObserver = new IntersectionObserver( (entries:IntersectionObserverEntry[]) => {
			if (!scrollContainer) {console.error('scroll container is missing')}

			entries.forEach( (entry) => {

				if (entry.isIntersecting) {
	
					const newHeader = document.createElement('h1')
					newHeader.innerText = "Created Scroll Down!"
					newHeader.className = 'created-element'

					const newImage = document.createElement('img')
					i = i+1
					newImage.src = `<img src="https://loremflickr.com/500/300?random=${i}" />`
					newImage.loading = 'lazy'

					scrollContainer?.appendChild(newHeader)
					scrollContainer?.appendChild(newImage)


					observer.observe(newImage)
					
				}
			})
		}, {
			threshold: 1
		})

		if (headers) {
			observer.observe(headers[0])
		} else {
			console.error('No Header Element!')
		}

	})



</script>

<main class="scroll-container">
	
	<h1 class='created-element'>Scroll Down!</h1>

	<div class="grid">
		<div class="image-container">
			<img class='created-image' src={`https://loremflickr.com/320/240?random=1`} alt='kitten' on:load={handleLoad}/>
		</div>
	</div>

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
		background-attachment: scroll;
	}

	.grid {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-template-rows: 1fr;
		gap: 1em;
		margin: 0 2em;
		place-items: center;
	}

	.image-container {
		background-color: grey;
	}

	.created-image {
		opacity: 0;
		transition: opacity .3s ease-in;
	}

	.created-element {
		position: relative;
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100%;
		transform-style: preserve-3d;
		z-index: -1;
		margin-top: 20vh;
		/* display: none; */
	}

</style>