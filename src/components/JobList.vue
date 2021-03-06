<template>
    <div class="p-8 flex flex-row space-x-6">
        <div class="w-1/2">
            <div class="mb-6">
                <signed-in @input="getUserProfile" v-if="isSignedIn" />
                <google-sign-in-button v-else />
            </div>
            <div v-for="(job, index) in jobs" :key="index" class="p-6 shadow bg-white space-y-4 md:space-y-1" :class="[{ '-mr-6 rounded-tr-none rounded-br-none border-l-8 border-blue-600 pl-4': index == activeIndex }, { 'mb-6': index != jobs.length - 1 }]">
                <div @click="previewPDF(job.pdf); setActiveIndex(index)" class="font-bold text-2xl mb-3 text-gray-600 cursor-pointer" :class="{ 'text-blue-600': index == activeIndex }">{{ job.position }}</div>
                <div class="flex flex-col md:flex-row space-x-2">
                    <label class="font-semibold w-full md:w-48 flex-shrink-0">Program: </label>
                    <div class="text-lg md:text-base m-0">{{ job.program }}</div>
                </div>
                <div class="flex flex-col md:flex-row space-x-2">
                    <label class="font-semibold w-full md:w-48 flex-shrink-0">Vacancy: </label>
                    <div class="text-lg md:text-base m-0">{{ job.vacancy }}</div>
                </div>
                <div class="flex flex-col md:flex-row space-x-2">
                    <label class="font-semibold w-full md:w-48 flex-shrink-0">Area of Assignment: </label>
                    <div class="text-lg md:text-base m-0">{{ job.area_of_assignment }}</div>
                </div>
                <div v-if="job.engagement_period" class="flex flex-col md:flex-row space-x-2">
                    <label class="font-semibold w-full md:w-48 flex-shrink-0">Period of Enagagement: </label>
                    <div class="text-lg md:text-base m-0">{{ job.engagement_period }}</div>
                </div> 
                <div class="flex flex-col md:flex-row space-x-2">
                    <label class="font-semibold w-full md:w-48 flex-shrink-0">Salary Grade: </label>
                    <div class="text-lg md:text-base m-0">{{ job.salary_grade }}</div>
                </div>
                <div class="flex flex-col md:flex-row space-x-2">
                    <label class="font-semibold w-full md:w-48 flex-shrink-0">Status: </label>
                    <div class="text-lg md:text-base m-0">{{ job.employment_status }}</div>
                </div>
                <div class="flex flex-col md:flex-row space-x-2">
                    <label class="font-semibold w-full md:w-48 flex-shrink-0">Deadline: </label>
                    <div class="text-lg md:text-base m-0">{{ job.deadline }}</div>
                </div>

                <div class="flex space-x-4">
                    <button @click="previewPDF(job.pdf); setActiveIndex(index)" class="text-blue-600 hover:text-blue-800 hover:underline mt-6 px-4 py-2 border rounded-sm">Details</button>
                    <apply-now :job-id="job.id" :profile="profile" />
                </div>
            </div>
        </div>
        <div v-if="pdf" class="w-1/2 max-h-screen sticky top-0 -mb-8" style="background-color: #d4d4d4">
            <iframe class="w-full h-full" :src="pdf"></iframe>
        </div>
    </div>
</template>

<script>
    import GoogleSignInButton from './GoogleSignInButton'
    import SignedIn from './Profile'
    import ApplyNow from './ApplyNow.vue'

    export default {
        props: {
            isSignedIn: Boolean
        },

        components: {
            GoogleSignInButton,
            SignedIn,
            ApplyNow,
        },

        data () {
            return {
                jobs: null,
                pdf: null,
                activeIndex: null,
                profile: null,
            }
        },

        methods: {
            parseData (entries) {
                return entries.map(function (value) {
                    return {
                        id: value.gsx$id.$t,
                        program: value.gsx$program.$t,
                        position: value.gsx$position.$t,
                        vacancy: value.gsx$vacancy.$t,
                        area_of_assignment: value.gsx$areaofassignment.$t,
                        engagement_period: value.gsx$engagementperiod.$t,
                        salary_grade: value.gsx$salarygrade.$t,
                        employment_status: value.gsx$employmentstatus.$t,
                        deadline: value.gsx$deadline.$t,
                        pdf: value.gsx$pdf.$t,
                    }
                })
            },

            previewPDF (pdfLink) {
                this.pdf = pdfLink
            },

            setActiveIndex (index) {
                this.activeIndex = index
            },

            signOut () {
                var auth2 = window.gapi.auth2.getAuthInstance();
                auth2.signOut().then(function () {
                    console.log('User signed out.');
                })
            },

            getUserProfile (value) {
                this.profile = value
            }
        },

        mounted () {
            fetch('https://spreadsheets.google.com/feeds/list/1owxa4OPotWmFzemDC5LnRVJB8i-ruG7x2XuZfRESrDM/1/public/values?alt=json').then(response => response.json()).then(data => this.jobs = this.parseData(data.feed.entry))
        }
    }
</script>