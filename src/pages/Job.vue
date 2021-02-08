<template>
	<div>
		Job
		<div v-for="(job, index) in jobs" :key="index">
			<div>{{ job.id }} {{ job.position }} {{ job.vacancy }}</div>
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
						position: value.gsx$position.$t,
						vacancy: value.gsx$vacancy.$t
					}
				})
			}
		},

		mounted () {
			fetch('https://spreadsheets.google.com/feeds/list/1owxa4OPotWmFzemDC5LnRVJB8i-ruG7x2XuZfRESrDM/1/public/values?alt=json').then(response => response.json()).then(data => this.jobs = this.parseData(data.feed.entry))
		}
	}
</script>