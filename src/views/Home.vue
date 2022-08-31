<template>
  <div class="home">
    <p ref="pRef">my name is:{{ name }} and my age is: {{ age }}</p>
    <p>
      Reactive refs can be output can be use as like this: learning
      {{ language }}
    </p>
  </div>
  <button @click="hanleClick">Click me</button>
  <!-- update refs value use v-model -->
  <input type="text" v-model="language" />
  <h2>Reactive reference</h2>
  <p>
    His name is: {{ reactiveVariable.name }} and age is:
    {{ reactiveVariable.age }}
  </p>
  <button @click="updateReactive">Update Reactive</button>
</template>

<script>
// @ is an alias to /src
//import Home from '@/components/Home.vue';
import { ref, reactive } from "vue";

export default {
  name: "Home",

  setup() {
    //create a ref in set up function
    const pRef = ref(null);

    //can create variables
    let name = "sophia";
    let age = 12;
    console.log("set up");

    //Reactive ref value
    const language = ref("Vue js");

    //use reactive
    const reactiveVariable = reactive({ name: "steven", age: 33 });

    //create reactive function to update value
    const updateReactive = () => {
      reactiveVariable.age = 23;
    };

    //can create functions
    const hanleClick = () => {
      //get the reference value of p tag
      console.log(pRef.value);

      //update reactive refs
      language.value = "updated reactive ref value";

      //can also add class name like nomal javaScript
      pRef.value.classList.add("new-class-name");

      //replace the value
      pRef.value.textContent = "This is ref text content";
    };

    //use reactive as reference DOES NOT need to .value

    //must return an object value,
    //if you want to used in template
    return {
      name,
      age,
      hanleClick,
      pRef,
      language,
      reactiveVariable,
      updateReactive,
    };
  },

  created() {},
  mounted() {},
};
</script>
