<template>
	<div>
		<nuxt />
	</div>
</template>

<script>
export default {
	head() {
		return {
			title: 'Ambient Soundboard',
			meta: [
				{
					charset: 'utf-8'
				},
				{
					name: 'viewport', 
					content: 'width=device-width, initial-scale=1'
				},
				{
					hid: 'description',
					name: 'description',
					content: 'Ambient sound board'
				}
			]
		}
	}
}
</script>


<style lang="sass">
@keyframes fadeIn
	0%
		opacity: 0
	100%
		opacity: 1
.hide
	display: none !important
@font-face
	font-family: 'Open Sans'
	src: url('../static/fonts/OpenSans-Regular.ttf') format('truetype')
	font-weight: normal
	font-style: normal
html
	font-family: 'Open Sans', sans-serif
	font-size: 14px
	-ms-text-size-adjust: 100%
	-webkit-text-size-adjust: 100%
	-moz-osx-font-smoothing: grayscale
	-webkit-font-smoothing: antialiased
	box-sizing: border-box
	transition: background 0.25s ease-in-out
	background: #ccc
*,
*:before,
*:after
	box-sizing: border-box
	font-size: 14px
	padding: 0
	margin: 0
	line-height: 1rem
	color: black
</style>
