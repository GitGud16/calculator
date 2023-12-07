<script>
import {onMount} from 'svelte';
 let result='';
 
let isComma=false
let regex=/[+\-*/]$/
let regexComma=/[.]$/;



let backspace=()=>{

    if(!result){
        console.log('empty');
    }else if(result){
        let temp='' 
        for(let i=0;i<result.length-1;i++){
            temp=temp+result[i]
        }
        if(result[result.length-1]==='.'){
            isComma=false
        }
        result=temp
    }
}

let dot =()=>{ 
    if (!result||regex.test(result)){
        result+='0.'
    }else if(regexComma.test(result)){
        console.log('no')
    }else if(isComma === false){
        result+='.';
         isComma=!isComma
        }
}
let operator=(operator)=>{
    if (!result){
    }else if(regex.test(result)||regexComma.test(result)){
       console.log('no') 
    }else{
        result+=operator
        isComma=false
    }
}

let calculate=()=>{
    if(regex.test(result) || regexComma.test(result)){
        console.log('cant calculate if operator or comma is the last thing you type')
    }else if(eval(result)){
        result=eval(result)
        if(result%1!==0){
            isComma=true
        }else if(result%1===0){
            isComma=false
        }
    }
}

onMount(()=>{
    window.addEventListener('keydown', handleKeydown)
})

function handleKeydown(event) {
    document.activeElement.blur();
    if (event.key === "Enter") { 
    calculate();
    }

    else if (event.key=== "Backspace"){
        backspace();
    }
    else if (event.key>= "0" && event.key<= "9" ){
        result += event.key
    }
    else if(event.key ==='*' || event.key ==='-' || event.key ==='/' || event.key ==='+'){
        operator(event.key)
    }
    else if(event.key ==='C' ||event.key ==='c' ){
        isComma=!isComma
        result=''
    }
    else if (event.key ==='.'){
       dot()

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
    <button on:click={()=>{isComma=!isComma;result=''}} class="grid-item">C</button>
    <button on:click={()=>result+='0'} class="grid-item">0</button>
    <button on:click={()=>dot()} class="grid-item">.</button><!--one comma only + no operator after comma -->
    <button on:click={calculate} class="grid-item">=</button> <!--calculation needed -->
   





  </div>

<style>
    .grid-container {
        display: grid;
        grid-template-columns:repeat(4,1fr);
        grid-template-rows:repeat(6,1fr);
        background-color: navy;
        padding: 10px;
        gap: 2px 9px;
        height: 65vh;
     max-width: 800px;
     min-width: 600px;
     min-height: 515px;
      }
      .grid-item {
        background-color: rgba(255, 255, 255, 0.755);
        border: 1px solid rgba(0, 0, 0, 0.8);
        padding: 20px;
        font-size: 30px;
        text-align: center;
        border-radius: 30%;
        cursor: pointer;
      }
      .screen{
        box-sizing: border-box;
        grid-column-start: span 3;
        grid-row-start: span 2;
        font-size:35px ;
      }
</style>