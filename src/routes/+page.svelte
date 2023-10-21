<script lang='ts'>

	import { onMount } from "svelte";

	let i = 1

	function handleLoad({currentTarget}: {currentTarget: HTMLElement}) {
		console.log('handleLoad')
		currentTarget.style.opacity = '100'
	}

	onMount(()=>{
		const scrollContainer = document.querySelector('.scroll-container')
		const observed = document.querySelectorAll('h1')

		const observer:IntersectionObserver = new IntersectionObserver( (entries:IntersectionObserverEntry[]) => {
			console.log('observed')
			if (!scrollContainer) console.error('scroll container is missing')

			entries.forEach( (entry) => {

				if (entry.isIntersecting) {
				
					observer.unobserve(entry.target)
					console.log('isIntersecting')
					const newHeader = document.createElement('h1')
					newHeader.innerText = "Scroll Down for MOAR CATS!"
					newHeader.style.textAlign = 'center'

					const newImageContainer = document.createElement('div')
					newImageContainer.className = 'image-container'
					newImageContainer.style.backgroundColor = 'Gray'
					const randomZValue = (Math.floor(Math.random() * 10) + 1) * -1
					const randomMarginIndex = Math.floor(Math.random() * 3)
					const marginOptions = [
						'0 auto 0 0',
						'0 0 0 auto',
						'0 auto',
					]
					newImageContainer.style.translate = `0 0 ${randomZValue}px`
					newImageContainer.style.display = `inline-block`
					newImageContainer.style.margin = `${marginOptions[randomMarginIndex]}`

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
			observer.observe(observed[0])
		} else {
			console.error('observe() error, no observed')
		}
	})

</script>

<main class="scroll-container">
	
	<h1 class='initial-header'>Scroll Down!</h1>

</main>

<style>

	* {
		font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
	}

	.scroll-container {
		position: fixed;
		inset: 0;
		overflow: hidden scroll;
		perspective: 10px;
		background-image: url("$lib/assets/puzzlePieces.webp");
		background-position: 50% 75%;
		background-attachment: scroll;
		display: flex;
		flex-direction: column;
	}

	.initial-header {
		position: relative;
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100%;
		transform-style: preserve-3d;
		z-index: -1;
		margin-top: 50vh;
		margin-bottom: 60vh;
	}

</style>