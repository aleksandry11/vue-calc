<template>
    <div class="calc">
        <h1 class="calc-title">{{title}}</h1>
        <input v-model.number="condition" type="number" class="calc-window" />
        <operations :first-operand="state.operand" :operation="state.type" :second-operand="state.secondOperand" :result="state.result"/>
        <div class="history">
            <button class="show">Show history</button>
        </div>
        <div class="calc-btns">
            <div class="calc-numbers">
                <div
                     class="calc-number__item"
                     v-for="item in numbers"  v-bind:key="item.value"
                     :class="item.value === 0 ? 'zero' : ''"
                     v-on:click="addNumber(item.value)">
                    {{item.title}}
                </div>
            </div>
            <div class="calc-actions">
                <div class="calc-action__item clear" @click="clear">C</div>
                <div class="calc-action__item" v-for="item in operations" v-bind:key="item.title" @click="operation(item.title)">
                    {{item.title}}
                </div>
                <div class="calc-action__item equal" @click="execute">=</div>
            </div>
        </div>
    </div>
</template>

<script>
    import operations from './operations';
    export default {
        name: "Calc",
        props: {
            title: String
        },
        components: {
            operations
        },
        methods: {
            addNumber: function (key) {
                let value = this.condition.toString() + key.toString();
                this.condition = parseInt(value, 10);
            },
            clear: function () {
                this.condition = '';
            },
            operation: function (type) {
                this.state.operand = this.condition;
                if (!this.state.operand) this.state.operand = this.state.result;
                this.state.type = type;
                this.condition = '';
            },
            execute: function () {
                this.state.secondOperand = this.condition;
                switch (this.state.type) {
                    case '+':
                        this.state.result = this.state.operand + this.state.secondOperand;
                        break;
                    case '-':
                        this.state.result = this.state.operand - this.state.secondOperand;
                        break;
                    case '*':
                        this.state.result = this.state.operand * this.state.secondOperand;
                        break;
                    case '/':
                        this.state.result = this.state.operand / this.state.secondOperand;
                        break;
                    default: break;
                }
                this.condition = '';
            }
        },
        data: () => {
            return {
                state: {
                    operand: null,
                    type: null,
                    secondOperand: null,
                    result: null
                },
                numbers:
                    [
                        { title: '1', value: 1},
                        { title: '2', value: 2},
                        { title: '3', value: 3},
                        { title: '4', value: 4},
                        { title: '5', value: 5},
                        { title: '6', value: 6},
                        { title: '7', value: 7},
                        { title: '8', value: 8},
                        { title: '9', value: 9},
                        { title: '0', value: 0},
                        { title: '.', value: '.'},
                    ],
                operations:
                    [
                        { title: '+'},
                        { title: '-'},
                        { title: '*'},
                        { title: '/'},
                    ],
                condition: ''
            }
        }
    }
</script>

<style scoped>
    .calc {

    }
    .calc-title {
        color: #339eb7;
        font-size: 60px;
        font-weight: 900;
    }

    .calc-window {
        background-color: #35495e;
        color: #03a9f4;
        border: 10px solid #1e2338;
        height: 100px;
        padding: 10px 20px;
        font-size: 70px;
        font-weight: 900;
        line-height: 55px;
        text-align: right;
        outline: none;
    }
    .calc-window::-webkit-inner-spin-button,
    .calc-window::-webkit-outer-spin-button {
        -webkit-appearance: none;
        margin: 0;
    }

    .show {
        border: none;
        background-color: #00bcd4;
        color: white;
        outline: none;
        border-radius: 3px;
        font-size: 24px;
        padding: 10px 20px;
        margin: 30px 0;
        cursor: pointer;
        transition: opacity 200ms ease;
    }
    .show:hover {
        opacity: .8;
    }

    .calc-btns {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .calc-numbers {
        display: grid;
        grid-template-columns: repeat(3, 70px);
        grid-template-rows: repeat(4, 70px);
        grid-gap: 2px;
        margin-right: 2px;
    }
    .calc-number__item, .calc-action__item {
        background-color: #1e2335;
        display: flex;
        justify-content: center;
        align-items: center;
        color: #339eb7;
        cursor: pointer;
        font-weight: bold;
        font-size: 20px;
        transition: background-color 200ms ease;
        border-radius: 2px;
        user-select: none;
    }
    .calc-action__item {

    }
    .calc-number__item:hover, .calc-action__item:hover {
        background-color: #22283e;
    }
    .calc-number__item.zero {
        grid-column: span 2;
    }
    .calc-actions {
        display: grid;
        grid-template-columns: repeat(2, 70px);
        grid-template-rows: repeat(4, 70px);
        grid-gap: 2px;
    }
    .calc-action__item.clear, .calc-action__item.equal {
        grid-row-start: span 1;
        grid-column-start: span 2;
    }

</style>