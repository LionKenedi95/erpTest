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
            <slot>
                <button
                    @click="_calc(preparedInput1, preparedInput2)"
                >
                    Calc()
                </button>
            </slot>
            <slot
                v-for="item of customCalcs"
                :name="`button-${item.id}`"
            >
                <button
                    :key="item.id"
                    @click="_calc(preparedInput1, preparedInput2, item.calc, item.validator, item.alertText)"
                >
                    {{ item.text }}
                </button>
            </slot>
        </div>
        <div id="output">
            {{ output }}
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            calc: {
                type: Function,
                default: (a,b) => a + b,
            },
            alertText: {
                type: String,
                default: 'Непредвиденная ошибка',
            },
            validator: {
                type: Function,
                default: () => true,
            },
            customCalcs: {
                type: Array,
                default: () => [],
                validator: (val) => {
                    if (val.length > 3) return false;
                    return val.reduce((memo, item) => {
                        if (!typeof(item) === 'object'
                            || !item.hasOwnProperty('id')
                            || !item.hasOwnProperty('show')
                            || !item.hasOwnProperty('calc')
                            || !typeof(item.calc) === 'function') memo = false;
                        return memo;
                    }, true);
                },
            },
        },
        data() {
            return {
                input1: 0,
                input2: 0,
                output: 0,
            };
        },
        computed: {
            preparedInput1() {
                return this.input1 ? parseInt(this.input1) : 0;
            },
            preparedInput2() {
                return this.input2 ? parseInt(this.input2) : 0;
            },
        },
        methods: {
            _calc(arg1, arg2, calc=this.calc, validator=this.validator, alertText=this.alertText) {
                if (validator(arg1, arg2)) {
                    this.output = calc(arg1, arg2);
                } else {
                    alert(alertText);
                }
            },
        },
    };
</script>
    
<style scoped>
    input {
        padding: .4rem .6rem;
        margin-bottom: .4rem;
        border: none;
        border-bottom: 1px solid black;
    }
    input:focus {
        border: none;
    }
    button {
        background: none;
        border: 1px solid grey;
        padding: .2rem .6rem;
        margin: .2rem;
    }
    #output {
        margin-top: 2rem;
        font-size: 1.2rem;
    }
</style>