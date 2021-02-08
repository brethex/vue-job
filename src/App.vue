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

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
