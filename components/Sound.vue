<template>
	<div class="sound" :id="`sound-${this.index}`" @click="play">
		<div class="sound-image-wrapper">
			<img class="sound-image" :class="{ 'inverted': image.invert }" :src="image.src" :alt="this.info.title">
		</div>
		<p class="sound-title" v-text="this.info.title"></p>
		<audio class="sound-audio hide" src="" controls></audio>
		<div class="sound-volume-wrapper">
			<input class="sound-volume" @change="changeVolume" disabled="true" type="range" name="volume" min="0" max="10" step="1" v-model="volume">
		</div>
	</div>
</template>

<script>
export default {
	name: "Sound",
	props: {info: {}, index: ""},
	data() {
		return {
			volume: 10,
			playing: false,
		}
	},
	computed: {
		image: function() {
			return {
				src: this.info.image_local !== null ? this.info.image_local : this.info.image_test,
				invert: this.info.image_lightness == "dark" ? false : true
			}
		}
	},
	methods: {
		changeVolume: function() {
			let sound = document.getElementById(`sound-${this.index}`).getElementsByTagName("audio")[0]
			sound.volume = parseFloat(this.volume / 10)
		},
		play: function(e) {
			let sound = document.getElementById(`sound-${this.index}`).getElementsByTagName("audio")[0]
			let volume = document.getElementById(`sound-${this.index}`).getElementsByClassName("sound-volume")[0]
			if (!e.target.classList.contains("sound-volume") && !e.target.classList.contains("sound-volume-wrapper")) {
				if (!this.playing) {
					if (!sound.src.indexOf(".mp3") > -1 && !sound.src.indexOf(".mp4") > -1) {
						sound.src = this.info.source
					}
					volume.disabled = false
					sound.play()
				} else if (this.playing) {
					volume.disabled = true
					sound.pause()
				}
				this.playing = !this.playing
			}
		}
	}
}
</script>

<style lang="sass">
.sound
	flex: 1
	margin: 0.5rem
	cursor: pointer
	min-width: 100%
	background: #eee
	display: flex
	flex-wrap: wrap
	align-items: center
	justify-content: center
	border-radius: 0.5rem
	transition: all 0.2s ease-in-out
	box-shadow: 0 0 0.5rem 0.25rem rgba(0, 0, 0, 0.1) inset
	@media (min-width: 28rem)
		min-width: 40%
		max-width: 50%
	@media (min-width: 40rem)
		min-width: 30%
	&:hover
		background: rgba(#eee, 1)
		box-shadow: 0 0 0.5rem 0.25rem rgba(0, 0, 0, 0.1) inset
		.sound-image-wrapper
			.sound-image
				transform: scale(1.25)
	.sound-image-wrapper
		width: 100%
		height: 5rem
		display: flex
		flex-wrap: wrap
		align-items: center
		justify-content: center
		transition: all 0.1s ease-in-out
		@media (min-width: 28rem)
			height: 8rem
		.sound-image
			width: 3rem
			height: 3rem
			padding: 1rem
			box-sizing: content-box
			transition: all 0.1s ease-in-out
			@media (min-width: 28rem)
				width: 5rem
				height: 5rem
			&.inverted
				filter: invert(1)
	.sound-title
		font-size: 1.25rem
		line-height: 1.25rem
		text-align: center
		display: flex
		flex-wrap: wrap
		align-items: center
		justify-content: center
		padding: 1rem 1rem 0.25rem 1rem
	.sound-volume-wrapper
		width: 100%
		padding: 1rem 0.5rem
		.sound-volume
			width: 100%
</style>
