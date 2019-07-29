<template>
    <div class="calc-history">
        <div class="calc-history__record" v-for="(item, index) in this.history" v-bind:key="index">
            <div class="calc-history__record-index">{{index + 1}}.</div>
            <div class="calc-history__record-info">
                <span class="operand first">{{item.first}}</span>
                <span class="operand operation">{{item.operation}}</span>
                <span class="operand second">{{item.second}}</span>
                <span class="operand equality">=</span>
                <span class="result">{{item.result}}</span>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "History",
        data: function() {
            return {
                history: JSON.parse(localStorage.getItem("logs")).reverse()
            }
        }
    }
</script>

<style scoped>
    .calc-history {
        padding: 20px;
    }
    .calc-history__record {
        font-size: 24px;
        border-bottom: 1px solid #1c2031;
        padding: 10px 20px;
        display: flex;
        justify-content: space-between;
        font-style: italic;
    }
    .calc-history__record-index {
        color: #373d52;
    }
    .calc-history__record:first-child {
        border-top: 1px solid #1c2031;
    }
    .calc-history__record .operand.first,
    .calc-history__record .operand.second,
    .calc-history__record .result {
        color: #0085c1;
    }
</style>