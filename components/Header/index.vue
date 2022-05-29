<template>
    <nav class="flex items-center justify-between shadow flex-wrap px-6">
        <div class="block lg:hidden p-2">
            <button class="flex items-center px-3 py-2 border rounded text-teal-200 border-teal-400 hover:text-white hover:border-white">
            <svg class="fill-current h-3 w-3" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><title>Menu</title><path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z"/></svg>
            </button>
        </div>
        <div class="w-full block md:hidden flex-grow lg:flex lg:items-center lg:w-auto">
            <div class="text-sm lg:flex-grow">
                <NuxtLink to="/random" class="block mt-4 lg:inline-block lg:mt-0 text-teal-200 hover:bg-blue-100 hover:text-white mr-2 p-3" :class="this.url == '/random' ? 'bg-blue-70 text-white' : 'bg-white text-black'">
                    Random
                </NuxtLink>
                <NuxtLink to="/types" class="block mt-4 lg:inline-block lg:mt-0 text-teal-200 hover:bg-blue-100 hover:text-white mr-2 p-3" :class="this.url == '/types' ? 'bg-blue-70 text-white' : 'bg-white text-black'">
                    Type
                </NuxtLink>
                <NuxtLink to="/about" class="block mt-4 lg:inline-block lg:mt-0 text-teal-200 hover:bg-blue-100 hover:text-white mr-2 p-3" :class="this.url == '/about' ? 'bg-blue-70 text-white' : 'bg-white text-black'">
                    About
                </NuxtLink>
            </div>
        </div>
    </nav>
</template>

<script>
export default {
    name: 'Header',
    computed: {
        url() {
            return this.$route.path
        }
    },
    created: function() {
        // console.log(this.url, "===")
    }
}
</script>

<style>

</style>