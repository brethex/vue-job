<template>
	<div>
		Job
		<div v-for="(job, index) in jobs" :key="index">
			<div>{{ job.id }}</div>
			<div>{{ job.program }}</div>
			<div>{{ job.position }}</div>
			<div>{{ job.vacancy }}</div>
			<div>{{ job.area_of_assignment }}</div>
			<div>{{ job.engagement_period }}</div>
			<div>{{ job.salary_grade }}</div>
			<div>{{ job.employment_status }}</div>
			<div>{{ job.deadline }}</div>
		</div>
	</div>
</template>

<script>
	export default {
		data () {
			return {
				jobs: null,
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
					}
				})
			}
		},

		mounted () {
			fetch('https://spreadsheets.google.com/feeds/list/1owxa4OPotWmFzemDC5LnRVJB8i-ruG7x2XuZfRESrDM/1/public/values?alt=json').then(response => response.json()).then(data => this.jobs = this.parseData(data.feed.entry))
		}
	}
</script>