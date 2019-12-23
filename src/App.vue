<template>
    <div id="app">
        <img title="Vue logo" src="./assets/logo.png">
        <CustomForm
            :customCalcs="customCalcs"
        />
    </div>
</template>

<script>
    import CustomForm from './components/CustomForm.vue'

    export default {
        name: 'app',
        components: {
            CustomForm
        },
        data() {
            return {
                customCalcs: [{
                    id: 'division',
                    calc: (arg1, arg2) => arg1 / arg2,
                    validator: (arg1, arg2) => arg2 != 0,
                    text: 'Div()',
                    alertText: 'Нельзя делить на нуль!'
                },{
                    id: 'multiplication',
                    calc: (arg1, arg2) => arg1 * arg2,
                    validator: (arg1, arg2) => {
                        if (arg2 == 0) alert('Умножение на ноль всегда даст ноль!');
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
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
