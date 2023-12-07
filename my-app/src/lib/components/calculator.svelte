<script>
import {onMount} from 'svelte';
 let result='';
 


let test=(operator)=>{
    
    console.log(operator);
// if(oper==='/'){

// }
}


let backspace=()=>{

    if(!result){
        console.log('empty');
    }else if(result){
        let temp='' 
        for(let i=0;i<result.length-1;i++){
            temp=temp+result[i]
        }
        result=temp
        
    }
}

let operator=(operator)=>{
let regex=/[+\-.*/]$/
    if (!result){
    }else if(regex.test(result)){
       console.log('no')
    // else if(result[result.length-1]===operator){
       
    }else{

        result+=operator
    }
}

let calculate=()=>{

    // let calculateArr=result.split(' ')
    // for (let i=0; i<calculateArr.length; i++) {
       
    // }
    result=eval(result)
//     let regex=/[+\-x/]/
//     let left
//     let right
//     let operator
//     let flag=false 
//     for (let i=0; i<result.length;i++){
//         if(result[i]!==regex){//make sure
//             if(flag===false){
//                 left.push(result[i])
//             }else{
//                 right.push(result[i])
//             }
//         } else if(result[i]===regex){//make sure
//             operator = result[i]
//             flag=!flag
//     }
// }
// let sum
//    sum= left+(operator)+right
// if(operator==='+'){

// }

}

onMount(()=>{
    window.addEventListener('keydown', handleKeydown)
})

function handleKeydown(event) {
    if (event.key === "Enter") { // Replace 'Enter' with the key you want
    calculate();
    }
  }

</script>


<div class="grid-container">
    <div class="grid-item screen">{result}</div>
    <button on:click={backspace} class="grid-item">Backspace</button>
    <button id="operator" on:click={()=>operator('/')} class="grid-item">/</button>  <!--calculation needed -->
    <button on:click={()=>result+='7'} class="grid-item">7</button>
    <button on:click={()=>result+='8'} class="grid-item">8</button>
    <button on:click={()=>result+='9'} class="grid-item">9</button>  
    <button id="operator" on:click={()=>operator('*')} class="grid-item">x</button><!--calculation needed + cant put 2 operators next to each other -->
    <button on:click={()=>result+='4'} class="grid-item">4</button>
    <button on:click={()=>result+='5'} class="grid-item">5</button>  
    <button on:click={()=>result+='6'} class="grid-item">6</button>
    <button id="operator" on:click={()=>operator('-')} class="grid-item">-</button> <!--calculation needed -->
    <button on:click={()=>result+='1'} class="grid-item">1</button>
    <button on:click={()=>result+='2'} class="grid-item">2</button>
    <button on:click={()=>result+='3'} class="grid-item">3</button>
    <button id="operator" value="+" on:click={()=>operator('+')} class="grid-item">+</button> <!--calculation needed -->
    <button on:click={()=>{result=''}} class="grid-item">C</button>
    <button on:click={()=>result+='0'} class="grid-item">0</button>
    <button on:click={()=>operator('.')} class="grid-item">.</button><!--one comma only + no operator after comma -->
    <button on:click={calculate} class="grid-item">=</button> <!--calculation needed -->
    <button on:click={()=>console.log(eval("10/5"))} class="grid-item">test</button> <!--calculation needed -->





  </div>

<style>
    .grid-container {
        display: grid;
        /* grid-template-columns: auto auto auto; */
        grid-template-columns:repeat(4,1fr);
        grid-template-rows:repeat(6,1fr);
        background-color: #2196F3;
        padding: 10px;
        gap: 2px 9px;
        /* width: 30vw; */
        height: 65vh;
     /* margin-left: 40%; */
     
   
      }
      .grid-item {
        background-color: rgba(255, 255, 255, 0.8);
        border: 1px solid rgba(0, 0, 0, 0.8);
        padding: 20px;
        font-size: 30px;
        text-align: center;
        
        /* cursor: pointer; */
      }
      .screen{
        box-sizing: border-box;
        grid-column-start: span 3;
        grid-row-start: span 2;
        font-size:35px ;
      }
</style>