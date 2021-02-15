<template>
	<div class="home">
		<job-list :is-signed-in="is_signed_in" />
	</div>
</template>

<script>
	import JobList from '@/components/JobList.vue'

	export default {
		name: 'Home',

		components: {
			JobList
		},

		data () {
			return {
				is_signed_in: false,
			}
		},

		methods: {
			initClient () {
				window.gapi.load('client:auth2', () => {
                    window.gapi.client.init({
                        'scope': 'https://www.googleapis.com/auth/spreadsheet',
                        'discoveryDocs': ['https://sheets.googleapis.com/$discovery/rest?version=v4']
                    }).then(() => {
                        const google_auth = window.gapi.auth2.getAuthInstance()
                        
                        this.is_signed_in = google_auth.isSignedIn.get()
                        google_auth.isSignedIn.listen(this.updateSignInStatus)
                    })
                })
			},

			updateSignInStatus (isSignedIn) {
				this.is_signed_in = isSignedIn
			}
		},

		mounted () {
			this.initClient()
		}
	}
</script>
