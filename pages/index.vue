<template>
	<div id="sounds">
		<div id="intro-overlay" @click="hideOverlay">
		<div id="intro-overlay-content">
			<p class="intro-overlay-content-para">Welcome!</p>
			<p class="intro-overlay-content-para">Take a moment to relax with with 54 ambient soundscapes in 5 sets</p>
		</div>
	</div>
		<div id="sounds-set-togglers">
			<p class="sounds-set-toggler" :class="{ 'active': i == 0 }" @click="changeSet" :data-setnum="i+1" v-for="(set, i) in 5" :key="`toggler-${i}`" v-text="i+1"></p>
		</div>
		<div id="sounds-wrapper">
			<div class="sounds-set" :class="{ 'hide': e > 0 }" :data-setnum="e+1" v-for="(set, e) in sounds" :key="`set-${e}`">
				<div class="sounds-set-list">
					<Sound v-for="(sound, a) in set.sounds" :key="`sound-${a}`" :info="sound" :id="`sound-${e}-${a}`" :index="`${e}-${a}`" />
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import Sound from '@/components/Sound'
import sounds from '@/assets/sounds_sets'
export default {
	components: {Sound},
	data() {
		return {
			sounds
		}
	},
	methods: {
		changeSet: function(e) {
			let set_number = e.target.dataset.setnum
			let togglers = [...document.getElementsByClassName("sounds-set-toggler")]
			for (let toggler of togglers) {
				toggler.classList.remove("active")
			}
			e.target.classList.add("active")
			let sets = [...document.getElementsByClassName("sounds-set")]
			let sets_len = sets.length
			for (let i = 0; i < sets_len; i++) {
				let num = sets[i].dataset.setnum
				if (num == set_number) {
					sets[i].classList.remove("hide")
				} else {
					sets[i].classList.add("hide")
				}
			}
		},
		hideOverlay: function() {
			let overlay = document.getElementById("intro-overlay")
			overlay.classList.add("hide")
		}
	}
}
</script>

<style lang="sass">
#sounds
	@include pageWrapper
	#intro-overlay
		height: 105vh
		width: 100%
		position: fixed
		top: -1rem
		left: 0
		z-index: 5
		display: flex
		flex-wrap: wrap
		align-items: center
		justify-content: center
		background: rgba(black, 0.5)
		#intro-overlay-content
			margin: 0.5rem 0.5rem 5rem 0.5rem
			display: flex
			flex-wrap: wrap
			align-items: center
			justify-content: center
			border-radius: 0.5rem
			background: #ddd
			.intro-overlay-content-para
				flex: 1
				text-align: center
				display: flex
				align-items: center
				justify-content: center
				min-width: 100%
				margin: 0.5rem
				padding: 1rem
				font-size: 1.5rem
				line-height: 1.5rem
	#sounds-set-togglers
		position: fixed
		bottom: 0
		left: 0
		z-index: 3
		width: 100%
		margin: 0 auto
		background: #bbb
		overflow: hidden
		display: flex
		flex-wrap: wrap
		align-items: center
		justify-content: center
		border-radius: 0 0 0.25rem 0.25rem
		.sounds-set-toggler
			flex: 1
			cursor: pointer
			padding: 0.5rem
			background: #ddd
			text-align: center
			display: flex
			flex-wrap: wrap
			align-items: center
			justify-content: center
			transition: background 0.25s ease-in-out
			box-shadow: 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.1) inset
			&:hover
				background: #eee
			&.active
				background: #eee
	#sounds-wrapper
		margin: 0.5rem
		padding: 0.5rem
		background: #ccc
		border-radius: 0.25rem
		.sounds-set
			.sounds-set-title
				width: 100%
			.sounds-set-list
				display: flex
				flex-wrap: wrap
				justify-content: center
				align-items: stretch
</style>
