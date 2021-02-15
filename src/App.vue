<template>
    <div id="app">
        <div id="nav" class="px-8">
            <router-link to="/">Home</router-link> |
            <router-link to="/about">About</router-link>
        </div>
        <router-view/>
    </div>
</template>

<script>
    export default {
        name: 'App',
    }
</script>

