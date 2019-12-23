<template>
    <div>
        <div>
            <input
                v-model="input1"
                type="number"
            >
        </div>
        <div>
            <input
                v-model="input2"
                type="number"
            >
        </div>
        <div>
            {{ output }}
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            func: {
                type: Function,
                default: (a,b) => a + b,
            },
        },
        data() {
            return {
                input1: 0,
                input2: 0,
            };
        },
        computed: {
            preparedInput1() {
                return this.input1 ? parseInt(this.input1) : 0;
            },
            preparedInput2() {
                return this.input2 ? parseInt(this.input2) : 0;
            },
            output() {
                return this.func(this.preparedInput1, this.preparedInput2);
            },
        }
    }
</script>
    
<style>
    
</style>