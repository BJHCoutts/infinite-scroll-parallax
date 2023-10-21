<script lang='ts'>
	import { onMount } from "svelte";

	let i = 1

	function handleLoad({currentTarget}: {currentTarget: HTMLElement}) {
		console.log('handleLoad')
		currentTarget.style.opacity = '100'
	}

	onMount(()=>{
		const scrollContainer = document.querySelector('.scroll-container')
		const observed = document.querySelectorAll('img')

		const observer:IntersectionObserver = new IntersectionObserver( (entries:IntersectionObserverEntry[]) => {
			console.log('observed')
			if (!scrollContainer) console.error('scroll container is missing')

			entries.forEach( (entry) => {

				if (entry.isIntersecting) {
				
					observer.unobserve(entry.target)
					console.log('isIntersecting')
					const newHeader = document.createElement('h1')
					newHeader.innerText = "Created Scroll Down!"
					newHeader.className = 'created-element'

					const newImageContainer = document.createElement('div')
					newImageContainer.className = 'image-container'
					newImageContainer.style.backgroundColor = 'Gray'

					const newImage = document.createElement('img')
					i = i+1
					newImage.className = 'created-image'
					newImage.style.transition = 'opacity 1s ease-in'
					newImage.style.opacity = '0'
					newImage.loading = 'lazy'
					newImage.src = `https://loremflickr.com/500/300?random=${i}`
					newImage.addEventListener( 'load', e => handleLoad(e))
					
					newImageContainer.appendChild(newImage)
					scrollContainer?.appendChild(newHeader)
					scrollContainer?.appendChild(newImageContainer)

					observer.observe(newImage)
					
				}
			})
		}, {
			threshold: 1
		})

		if (observed) {
			console.log(observed[0])
			observer.observe(observed[0])
		} else {
			console.error('observe() error, no observed')
		}



	})



</script>

<main class="scroll-container">
	
	<h1 class='created-element'>Scroll Down!</h1>

	<div class="grid">
		<div class="grid-cell left">
			<div class="image-container">
				<img class='created-image' src={`https://loremflickr.com/320/240?random=1`} alt='kitten' on:load={e => handleLoad(e)}/>
			</div>
		</div>
		<div class="grid-cell right"></div>
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

	.grid-cell {
		position: relative;
	}

	.image-container {
		background-color: grey;
	}

	.created-image {
		opacity: 0;
		transition: opacity 1s ease-in;
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