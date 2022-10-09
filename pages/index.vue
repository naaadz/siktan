<template>
	<main class="container mx-auto pt-48 pb-20 space-y-20">
		<div class="flex justify-center">

			<span class="mat-ico but text-8xl">navigate_before</span>
			
			<span  v-if="data.isPaused || data.isEnded" class="mat-ico but text-8xl" @click.prevent="pushPlay()">
				play_circle_outline
			</span>

			<span v-if="data.isPlaying" class="mat-ico but text-8xl" @click.prevent="pushPause()">
				pause_circle_outline
			</span>

			<span class="mat-ico but text-8xl">navigate_next</span>
		</div>
	</main>
</template>


<script setup>

	const data = reactive({
		player: null,
		currentIndex: 0,
		shuffleOn: false,
		isPaused: true,
		isPlaying: false,
		isEnded: false
	})

	const audioArray = computed(() => {
		const max = 50
		let arr = []

		for (let i = 0; i < max; i++) {
			arr[i] = i
		}

		return arr

	})

	const pushPlay = () => {
		data.player.play()
	}

	const pushPause = () => {
		data.player.pause()
	}

	const pushNext = () => {

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
	}

	.orange {
		color: orange;
	}

	.red {
		color: red;
	}
</style>