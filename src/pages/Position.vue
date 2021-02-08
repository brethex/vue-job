<template>
	<div>
		Position
		<div v-for="(position, index) in positions" :key="index">
			<div>{{ position.id }} {{ position.name }}</div>
		</div>
	</div>
</template>

<script>
	export default {
		data () {
			return {
				positions: null,
			}
		},

		methods: {
			parseData (entries) {
				return entries.map(function (value) {
					return {
						id: value.gsx$id.$t,
						name: value.gsx$position.$t,
					}
				})
			}
		},

		mounted () {
			fetch('https://spreadsheets.google.com/feeds/list/1L9YUmwU1qzgEMGH4CCmW_wbljEuw_5uHgHCF1ZCp38k/1/public/values?alt=json').then(response => response.json()).then(data => this.positions = this.parseData(data.feed.entry))
		}
	}
</script>