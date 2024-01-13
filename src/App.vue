<template>
    <div class="calculator">
        <p>{{ value }} {{ operator }} {{ prevValue }}</p>
        <div class="numbers">
            <button @click="changeValue(1)">1</button>
            <button @click="changeValue(2)">2</button>
            <button @click="changeValue(3)">3</button>
            <button @click="changeValue(4)">4</button>
            <button @click="changeValue(5)">5</button>
            <button @click="changeValue(6)">6</button>
            <button @click="changeValue(7)">7</button>
            <button @click="changeValue(8)">8</button>
            <button @click="changeValue(9)">9</button>
            <button @click="changeValue(0)">0</button>
        </div>
        <div class="operators">
            <button @click="setOperator('+')">+</button>
            <button @click="setOperator('-')">-</button>
            <button @click="setOperator('*')">*</button>
            <button @click="setOperator('/')">/</button>

            <button @click="count()">=</button>
            <button @click="clear()">ac</button>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
export default defineComponent({
    setup(){
        //* variables
        const value = ref<number>(0)
        const prevValue = ref<number>(0)
        const isPrevValue = ref<boolean>(false)
        const operator = ref<string>("")

        //* functions
        function changeValue(add: number){
            value.value = (value.value * 10) + add
        }

        function setOperator(operatorButton: string){
            operator.value = operatorButton
            if(isPrevValue){
                count()
            }
            prevValue.value = value.value
            value.value = 0
            isPrevValue.value = true
        }

        function count(){
            if(operator.value == "+"){
                value.value = prevValue.value + value.value
                prevValue.value = 0
                isPrevValue.value = false
                operator.value = ''
            }else if(operator.value == "-"){
                value.value = prevValue.value - value.value
                prevValue.value = 0
                isPrevValue.value = false
                operator.value = ''
            }else if(operator.value == "*"){
                value.value = prevValue.value * value.value
                prevValue.value = 0
                isPrevValue.value = false
                operator.value = ''
            }else if(operator.value == "/"){
                value.value = prevValue.value / value.value
                prevValue.value = 0
                isPrevValue.value = false
                operator.value = ''
            }
        }

        function clear(){
            value.value = 0
            prevValue.value = 0
            isPrevValue.value = false
            operator.value = ''
        }

        return{
            // vars
            value, prevValue, operator,
            // functions
            changeValue, setOperator, count, clear
        }
    }
})
</script>

<style>
p{
    font-size: 32px;
}

button{
    padding: 15px;
}
</style>
