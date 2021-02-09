<template>
    <div id="app">
        <job-list />
    </div>
</template>

<script>
    import JobList from './pages/Job.vue'

    export default {
        name: 'App',
        components: {
            JobList
        }
    }
</script>
