<template>
    <div class="calc">
        <div class="display">{{result || 0}}</div>
        <div class="btn clear" @click="clear">C</div>
        <div class="btn operator" @click="per">%</div>
        <div class="btn" @click="append(7)">7</div>
        <div class="btn" @click="append(8)">8</div>
        <div class="btn" @click="append(9)">9</div>
        <div class="btn operator" @click="divide">/</div>
        <div class="btn" @click="append(4)">4</div>
        <div class="btn" @click="append(5)">5</div>
        <div class="btn" @click="append(6)">6</div>
        <div class="btn operator" @click="multiply">x</div>
        <div class="btn" @click="append(1)">1</div>
        <div class="btn" @click="append(2)">2</div>
        <div class="btn" @click="append(3)">3</div>
        <div class="btn operator" @click="subtract">-</div>
        <div class="btn" @click="append(0)">0</div>
        <div class="btn" @click="dot">.</div>
        <div class="btn" @click="equal">=</div>
        <div class="btn operator" @click="sum">+</div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            result: '',
            prev: null,
            operator: null,
            operatorClick: false
        }   
    },
    methods :{
        clear(){
            this.result = '';
        },
        per(){
            this.result = parseFloat(this.result)/100;
        },
        append(number){
            this.result = this.result+number;
            if(this.operatorClick){
                this.result = '';
                this.operatorClick = false;
            }
        },
        dot(){
            if(this.result.indexOf('.') === -1)
            this.append('.');
        },
        divide(){
            this.operator = (a,b) => b/a;
            this.setPrev();
        },
        multiply(){
            this.operator = (a,b) => a*b;
            this.setPrev();
        },
        subtract(){
            this.operator = (a,b) => b-a;
            this.setPrev();
        },
        sum(){
            this.operator = (a,b) => a+b;
            this.setPrev();
        },
        equal(){
            this.result = this.operator(
                parseFloat(this.result),
                parseFloat(this.prev)
            );
            this.prev=null;
        },
        setPrev(){
            this.prev= this.result;
            this.operatorClick = true;
        }
    }
}
</script>

<style>
    *{
        
        border-radius: 8px;
        background: #2f3336;
    }
    .calc{
        width: 400px;
        margin: 0 auto;
        font-size: 38px;
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-auto-rows: minmax(auto,auto);
        border: 20px groove #2294e0;
        border-radius: 8px;
    }
    .display{
        grid-column: 1/5;
        background: #d1ebff;
        color: #141d24;
        padding: 20px;
        text-align: right;
    }
    .clear{
        grid-column: 1/4;
    }
    .btn{
        padding: 10px;
        color: #fafafa;
        background: linear-gradient(#0c3152,#22527d);
        border : 1px solid #999;
        cursor: pointer;
    }
    .btn:active{
        background: #fff;
        color: #777;
    }
    .operator{
        color: #47eaed;
    }


</style>