<template>
    <div id="app" class="h-screen">
        <div id="calc">
            <h1 class="text-center font-bold text-2xl mb-4 text-gray-900">
                Vue.js Calculator
            </h1>
            <Calculator />
            <h2 class="text-center font-mono mt-4 text-sm text-gray-900">
                created by
                <a href="https://mrpbennett.com" class="hover:underline"
                    >@mrpbennett</a
                >
            </h2>
        </div>
    </div>
</template>

<script>
    import Calculator from './components/Calc.vue';

    export default {
        name: 'App',
        components: {
            Calculator,
        },
    };
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        display: grid;
        place-items: center;
        background-image: linear-gradient(to top, #fff1eb 0%, #ace0f9 100%);
    }
</style>
