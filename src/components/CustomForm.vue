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
        <div>
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
                default: (a,b) => a && b,
            },
            customCalcs: {
                type: Array,
                default: () => [],
                validator: (val) => {
                    let check = true;
                    val.map(item => {
                        if (!typeof(item) === 'object' && !item.id && !item.calc) check = false;
                    });
                    return check;
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
</style>