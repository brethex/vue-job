<template>
	<div id="my-signin2"></div>
</template>

<script>
	export default {
		methods: {
			renderButton () {
				window.gapi.signin2.render('my-signin2', {
					'scope': 'profile email',
					'width': 240,
					'height': 50,
					'longtitle': true,
					'theme': 'dark',
					'onsuccess': this.onSuccess,
					'onfailure': this.onFailure
				})
			},

			onSuccess (googleUser) {
				console.log('Logged in as: ' + googleUser.getBasicProfile().getName())
			},

			onFailure (error) {
				console.log(error)
			}
		},

		mounted () {
			this.renderButton()
		},
	}
</script>