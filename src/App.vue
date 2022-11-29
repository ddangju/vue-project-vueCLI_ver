<template>
  <div>
    {{ name }}
  </div>
  <button class="btn btn-primary" v-on:click="handleClick">Click</button>
</template>

<script>
import {ref} from "vue";
export default {
  // composition api 
  setup(){
    // 필요한 로직작성하기
    let name = ref("yeonju");
    // const foo = (arg) =>{
    //   return arg
    // }
    // const greet = foo(name)
    console.log(name,"<nbame")
    const handleClick =()=>{
      name.value = "babo"
      // 바뀐 변수가 리랜더가 되지 않음.
    }
    return {
      name,
      handleClick
    }
  }
}
</script>

<style>

</style>
