<template>
    <div class="operations">
        <span class="operand first">{{firstOperand}}</span>
        <span class="operand operation">{{operation}}</span>
        <span class="operand second">{{secondOperand}}</span>
        <span v-if="result" class="operand equality">=</span>
        <span class="result">{{result}}</span>
    </div>
</template>

<script>
    export default {
        name: "operations",
        props: ['firstOperand', 'operation', 'secondOperand', 'result']
    }
</script>

<style>
    .operations {
        text-align: right;
        margin: 20px 0;
        font-size: 30px;
        color: #0085c1;
    }
    .operand {
        margin: 0 10px;
    }
    .operand.operation, .operand.equality {
        color: #41b883;
    }
    .operand.equality {
        color: #41b883;
    }
</style>