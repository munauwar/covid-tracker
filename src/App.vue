<template>
    <Header />
    <div class="container text-center">
        <router-view />
    </div>
</template>

<script>
import Header from '@/components/Header.vue'

export default {
    components: {
        Header
    },
}
</script>
