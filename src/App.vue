<template>
  <!-- <div>
    {{ name }}
  </div>
  <button class="btn btn-primary" v-on:click="handleClick">Click</button>
  <button class="btn btn-primary" @:click="upCounte">click</button>
  <h1>{{ counter[0] }}</h1>
  <p>{{name2}}</p> -->
  <p>{{teacher.name}}</p>
  <p>강의가 존재하는지</p>
  <div>{{ hasLectures }}</div>
  <p>{{ fullName }}</p>
  <div class="text" v-bind:class="{active:isActive}">text임</div>
</template>

<script>
import {onBeforeMount, onMounted, onUnmounted, onUpdated, reactive, computed, ref} from "vue";
export default {
  // composition api 
  //setup()함수로 맵핑(반응형dddapi사용,)
  setup(){
    const isActive = ref(true);
    // 필요한 로직작성하기
    // let name = ref("yeonju");
    // const counter = reactive([1,2]);
    // console.log(name,"<ref")
    // console.log(counter,"<reactive")
    // const foo = (arg) =>{
    //   return arg
    // }
    // const greet = foo(name)
    // const handleClick =()=>{
    //   name.value = "babo"
    //   // 바뀐 변수가 리랜더가 되지 않음.
    // }
    // const upCounte=()=>{
    //   counter
    // }
    // const info = reactive({
    //   name2:"kim",
    //   age: 15,
    // })

  // toRefs속성을 사용하여 구조분해 할당을 해야지 참조값을 그대로 가져온다.
    // const {name2, age} = toRefs(info)
  // 객체 내부에서 하나만 가져오고 싶다면?
    // const name2 = toRef(info,"name2")

    ///computed 
    const teacher = reactive({
      name: "jim",
      lectures : [
        "html/css",
        "java",
        "c+"
      ]
    })
    const hasLectures = computed(()=>{
      return teacher.lectures.length > 0 ? "ok" : "not ok"
    })
    const firstName = ref("김")
    const lastName = ref("연주")
    // const fullName = computed(()=>{ return firstName.value + lastName.value})
    // fullName.value = "주"
    const fullName = computed({
      // 기본은 getter이다.
      get() {
        return firstName.value + lastName.value
      },
      set(value) {
        //2 set함수에 새롭게 할당된 value가 넘어온다.하지만? 템플릿엔 샤로 할당된 value값으로 바뀌지 않았다.
        // console.log(value,"value")
        //3 새로운 value값을 split으로 쪼갠다! => 배열로 반환.
        // 4. ref(반응형)의 값들이 바뀌면서 get함수가 실행되어 리랜더가 되었음.
        [firstName.value, lastName.value] = value.split('')
        console.log(firstName, lastName,"<")
        return value
      }
    })
    //1. fullname의 value에 접근하여 다른 값으로 할당한다.
    // console.log(fullName,"<name")
    fullName.value = "고 양이"
    
    ////lifecycle
    onMounted(()=>{
      // console.log("component가 dom에 마운트 된 직후.")
    })
    onBeforeMount(()=>{
      // console.log("component가 dom에 마운트 되기 전.")
    })
    onUpdated(()=>{
      // console.log("component가 update(state가 변경)")
    })
    onUnmounted(()=>{
      // console.log("unmounted")
    })
    
    return {
      // name,
      // handleClick,
      // upCounte,
      // counter,
      // name2,
      teacher,
      hasLectures,
      fullName,
      isActive
    }
  }
  ///option api의 경우
  // data(){}
  // methods(){}
  // mounted(){}로 컴포넌트를 설정한다. 

}
</script>

<style>
.active{
  color:red;
}

</style>
