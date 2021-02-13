<template>
    <div>
        <button @click="initClient" class="text-blue-600 hover:text-blue-800 hover:underline mt-6 px-4 py-2 border rounded-sm">Apply Now</button>
    </div>
</template>

<script>
    export default {
        props: {
            jobId: [Number, String],
        },

        methods: {
            applyNow () {
                window.gapi.client.sheets.spreadsheets.values.append({
                    spreadsheetId: '1iDtUY4TRVfF-gsL-PhzqvEJkg4MA7LMavWoK7ehEOVM',
                    range: 'A1',
                    valueInputOption: "USER_ENTERED",
                    values: [
                        [
                            "",
                            this.jobId,
                            "",
                            ""
                        ]
                    ]
                }).then(function (response) {
                    console.log(response.result)
                }, function(reason) {
                    console.error('error: ' + reason.result.error.message);
                })
            },

            initClient () {
                window.gapi.load('client', this.applyNow())
            }
        }
    }
</script>