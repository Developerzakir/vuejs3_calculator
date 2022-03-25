<template>
  <div class="py-3" style="max-width:400px; margin:50px auto; background:#234; ">

    <!-- calculator Result here -->

    <div class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-dark" style="text-align:end">
        {{calculatorValue || 0}}
    </div>

    <!-- calculators button create -->

    <div class="row no-gutters">
      <div class="col-3" v-for="n in calculatorElements" :key="n">

        <div class="lead text-light text-center m-1 py-3 bg-dark rounded hover-class"

           :class="{'bg-cal-vue': ['C', '*', '/', '-', '+', '%', '='].includes(n)}"

           @click="action(n)"
        
        >
                {{n}}

        </div>

  

      </div>

    </div>
    
  </div>
</template>

<script>
export default {
  name: 'Calculator',

  data(){
    return{
      calculatorValue: '',
      calculatorElements: ['C', '*', '/', '-', 7,8,9, '+', 4,5,6, '%', 1,2,3, '=', 0, '.'],
      operator: null,
      previouscalculatorValue:'',
    }
  },


  methods:{

    action(n){

      // append value

      if(!isNaN(n) || n === '.'){
        this.calculatorValue += n + '';
      }

      // clear value

      if(n === 'C'){
        this.calculatorValue = '';
      }

      //percentage 

      if(n === '%'){
        this.calculatorValue = this.calculatorValue / 100 + '';
      }


      //  operator result

      if(['/', '*', '-', '+'].includes(n)){
        this.operator = n;

        this.previouscalculatorValue = this.calculatorValue;

        this.calculatorValue = '';
      }

      if(n==='='){
        this.calculatorValue = eval(
          this.previouscalculatorValue + this.operator + this.calculatorValue

        );

        this.previouscalculatorValue = '';
        this.operator = null;


      }



    }

  }
  
}
</script>


<style scoped>

.hover-class:hover{
  cursor:pointer;
 
}

.bg-cal-vue{
  background: green;
}

</style>
