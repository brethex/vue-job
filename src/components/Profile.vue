<template>
	<div class="flex bg-white justify-between shadow rounded-sm">
		<div class="flex space-x-4 px-4 py-2 items-center">
			<img alt="profile" class="rounded-full h-9 w-9" :src="profile.image_url">
			<div>
				<div>{{ profile.full_name }}</div>
				<div class="text-sm text-gray-400">{{ profile.email }}</div>
			</div>
		</div>
		<button @click.prevent="signOut" class="hover:text-blue-700 hover:underline px-4 py-2">Sign Out</button>
	</div>
</template>

<script>
	export default {
		data () {
			return {
				profile: {
					full_name: null,
					given_name: null,
					family_name: null,
					image_url: null,
					email: null,
				},
			}
		},

		methods: {
			getProfile () {
				const authInstance = window.gapi.auth2.getAuthInstance()
				const user = authInstance.currentUser.get()
				const profile = user.getBasicProfile()

				this.profile.full_name = profile.getName()
				this.profile.given_name = profile.getGivenName()
				this.profile.family_name = profile.getFamilyName()
				this.profile.image_url = profile.getImageUrl()
				this.profile.email = profile.getEmail()				
			},

            signOut () {
                const auth2 = window.gapi.auth2.getAuthInstance();
                auth2.signOut().then(function () {
                    console.log('User signed out.');
                })
            },

			initAuth2 () {
				window.gapi.load('auth2', this.getProfile())
			}
		},

		mounted () {
			this.initAuth2()
		}
	}
</script>