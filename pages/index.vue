<template>
	<main class="container mx-auto py-20 space-y-14">
		<div class="flex justify-center">

			<span class="mat-ico but text-8xl" @click="pushPrev()">navigate_before</span>
			
			<span  v-if="data.isPaused || data.isEnded" class="mat-ico but text-8xl" @click.prevent="pushPlay()">
				play_circle_outline
			</span>

			<span v-if="data.isPlaying" class="mat-ico but text-8xl" @click.prevent="pushPause()">
				pause_circle_outline
			</span>

			<span class="mat-ico but text-8xl" @click="pushNext()">navigate_next</span>
		</div>
		<span class="mat-ico but text-6xl block text-center" @click.prevent="pushShuffle()">
			{{ data.shuffleOn ? 'shuffle_on' : 'shuffle' }}
		</span>
	</main>
</template>


<script setup>

	const data = reactive({
		player: null,
		currentIndex: 0,
		maxIndex: 49,
		shuffleOn: false,
		isPaused: true,
		isPlaying: false,
		isEnded: false
	})

	const pushPlay = () => {
		data.player.play()
	}

	const pushPause = () => {
		data.player.pause()
	}

	const setShuffledIndex = () => {
		const rando = Math.floor(Math.random() * data.maxIndex)
		data.currentIndex = rando
		console.log('currentIndex', data.currentIndex)
	}

	const pushPrev = () => {
		if (data.shuffleOn) {
			setShuffledIndex()
		} else {
			if (data.currentIndex === 0) { 
				data.currentIndex = data.maxIndex
			} else {
				data.currentIndex --
			}
		}
		
		console.log('currentIndex', data.currentIndex)
		data.player.src = `./assets/audio/Recording (${data.currentIndex}).m4a`
		pushPlay()
	}

	const pushNext = () => {
		if (data.shuffleOn) {
			setShuffledIndex()
		} else {
			if (data.currentIndex < data.maxIndex) {
				data.currentIndex ++
			} else {
				data.currentIndex = 0
			}
		}

		console.log('currentIndex', data.currentIndex)
		data.player.src = `./assets/audio/Recording (${data.currentIndex}).m4a`
		pushPlay()
	}

	const pushShuffle = () => {
		data.shuffleOn ? data.shuffleOn = false : data.shuffleOn = true
	}

	onMounted(() => {
		data.player =  new Audio()
		data.player.src = `./assets/audio/Recording (${data.currentIndex}).m4a`

		data.player.addEventListener('play', () => {
			data.isPlaying = true
			data.isPaused = false
		})

		data.player.addEventListener('pause', () => {
			data.isPaused = true
			data.isPlaying = false
		})

		data.player.addEventListener('end', () => {
			data.isEnded = true
			data.isPaused = false
			data.isPlaying = false
		})

		//console.dir(data.player)
	})	

</script>

<style lang="scss">
	.but {
		cursor: pointer;
		transition: opacity .5s;

		// &:hover {
		// 	opacity: .5;
		// }
	}

	.orange {
		color: orange;
	}

	.red {
		color: red;
	}
</style>