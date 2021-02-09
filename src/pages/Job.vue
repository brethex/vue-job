<template>
	<div class="m-8">
		<div v-for="(job, index) in jobs" :key="index" class="p-6 md:w-1/2 mx-auto rounded shadow mb-6 bg-white space-y-4 md:space-y-1">
			<a v-if="job.pdf" :href="job.pdf" target="_blank" rel="noopener noreferrer" class="font-bold text-2xl mb-3 text-blue-600">{{ job.position }}</a>
			<div v-else class="font-bold text-2xl mb-3 text-gray-600">{{ job.position }}</div>
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
						pdf: value.gsx$pdf.$t,
					}
				})
			}
		},

		mounted () {
			fetch('https://spreadsheets.google.com/feeds/list/1owxa4OPotWmFzemDC5LnRVJB8i-ruG7x2XuZfRESrDM/1/public/values?alt=json').then(response => response.json()).then(data => this.jobs = this.parseData(data.feed.entry))
		}
	}
</script>