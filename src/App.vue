<template>
    <div id="app">
        <div id="nav" class="px-8">
            <router-link :to="{ path: '/', params: { is_signed_in: is_signed_in } }">Home</router-link> |
            <router-link to="/about">About</router-link>
        </div>
        <router-view/>
    </div>
</template>

<script>
    export default {
        name: 'App',

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
                        this.is_signed_in = true

                        google_auth.isSignedIn.listen(this.updateSignInStatus)
                    })
                })
            },

            updateSignInStatus (isSignedIn) {
                this.is_signed_in = isSignedIn
            },
        },

        mounted () {
            this.initClient()
        }
    }
</script>

