<template>
    <div>
        <!-- Pokemon page -->
        <!-- Here we will show info about each pokemon -->
    </div>
</template>

<script setup>

import {useRoute} from "vue-router"

const route = useRoute()

// passing name as route parameter. Check router/index.js for more details
console.log(route.params.name)

</script>

