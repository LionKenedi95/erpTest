<template>
    <div id="app">
        <img title="Vue logo" src="./assets/logo.png">
        <Calculator
            :customCalcs="customCalcs"
        />
    </div>
</template>

<script>
    import Calculator from './components/Calculator.vue'

    export default {
        name: 'app',
        components: {
            Calculator
        },
        data() {
            return {
                customCalcs: [{
                    id: 'division',
                    show: true,
                    calc: (arg1, arg2) => arg1 / arg2,
                    validator: (arg1, arg2) => arg1 != 0 && arg2 != 0,
                    text: 'Div()',
                    alertText: 'Нельзя делить на нуль!'
                },{
                    id: 'multiplication',
                    show: true,
                    calc: (arg1, arg2) => arg1 * arg2,
                    validator: (arg1, arg2) => {
                        if (arg2 == 0) alert('Умножение на нуль всегда даст нуль!');
                        return true;
                    },
                    text: 'Multi()',
                }],
            }
        }
    }
</script>

<style>
    #app {
        font-family: Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
