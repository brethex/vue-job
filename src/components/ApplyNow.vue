<template>
    <div>
        <button @click="applyNow" class="text-blue-600 hover:text-blue-800 hover:underline mt-6 px-4 py-2 border rounded-sm">Apply Now</button>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                params: {
                    spreadsheetId: '1owxa4OPotWmFzemDC5LnRVJB8i-ruG7x2XuZfRESrDM',
                    range: 'Sheet1!'
                }
            }
        },

        methods: {
            applyNow () {
                window.gapi.client.sheets.spreadsheets.values.append({
                    spreadsheetId: '1owxa4OPotWmFzemDC5LnRVJB8i-ruG7x2XuZfRESrDM',
                    range: 'Sheet1!A1'
                }, {

                }).then(function (response) {
                    console.log(response.result)
                }, function(reason) {
                    console.error('error: ' + reason.result.error.message);
                })
            },

            initClient () {
                window.gapi.client.init({
                    apiKey: 'AIzaSyC3e2WUAyYYqrGNqS7dbfuEpIKbW4xNzVk',
                    clientId: '300681291290-kjapaj6tkl7na1nrs9igms0ph2hlqbtj.apps.googleusercontent.com',
                    discoveryDocs: ["https://sheets.googleapis.com/$discovery/rest?version=v4"],
                    scopes: "https://www.googleapis.com/auth/spreadsheets"
                }).then(function () {
                    console.log(window.gapi.auth2.getAuthInstance().isSignedIn.get())
                })
            },

            handleClientLoad () {
                window.gapi.load('client:auth2', this.initClient)
            }
        },

        mounted () {
            this.handleClientLoad()
        }
    }
</script>