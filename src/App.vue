<template>
    <div id="app">
        <div id="nav">
            <router-link to="/">Home</router-link> |
            <router-link to="/about">About</router-link>
        </div>
        <router-view/>

        <job-list />
    </div>
</template>

<script>
    import JobList from './components/JobList.vue'

    export default {
        name: 'App',

        components: {
            JobList
        },

        methods: {
            profile () {
                window.gapi.load('client:auth2', () => {
                    window.gapi.client.init({
                        'scope': 'https://www.googleapis.com/auth/spreadsheet',
                        'discoveryDocs': ['https://sheets.googleapis.com/$discovery/rest?version=v4']
                    }).then(() => {
                        window.gapi.auth2.getAuthInstance()
                    })
                })
            },
        },

        mounted () {
            this.profile()
        }
    }
</script>

