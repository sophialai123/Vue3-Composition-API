<template>
  <div class="home">
    <!-- pass bind posts data from set up  -->
    <PostList v-if="showPost" :posts="posts" />
    <!-- toggle show post button  -->
    <button
      @click="showPost = !showPost"
      :style="{ backgroundColor: 'green', 'font-size': '24px', color: 'white' }"
    >
      Toggle post
    </button>
    <button @click="deletePost">Pop the last post</button>
    <!-- reps -->
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

  <h1>How to use computed proprety inside of setup</h1>
  <input type="text" v-model="search" />
  <h3>Searching fruit is: {{ search }}</h3>
  <div v-for="fruit in filteredFruits" :key="fruit">{{ fruit }}</div>

  <button @click="callStopWatchFun">Stop watch function</button>
</template>

<script>
// @ is an alias to /src
//import Home from "@/components/Home.vue";
import { ref, reactive, computed, watch, watchEffect } from "vue";
import PostList from "../components/PostList.vue";

export default {
  name: "Home",
  components: { PostList },
  setup() {
    //toggle the post
    const showPost = ref(true);

    //pop the last post
    const deletePost = () => {
      return posts.pop();
    };

    //Post list data
    const posts = [
      {
        id: 1,
        title: "React learning",
        body: "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.",
      },
      {
        id: 2,
        title: "Vue js learning",
        body: "Letraset sheets containing Lorem Ipsum passages",
      },
      {
        id: 3,
        title: "Node js learning",
        body: "more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum",
      },
      {
        id: 4,
        title: "C# learning",
        body: "Lorem Ipsum has been the industry's standard dummy text ever since the 1500s",
      },
    ];

    const fruits = ref([
      "apples",
      "oranges",
      "bananas",
      "blueberries",
      "pears",
    ]);
    const search = ref("");
    //filtered fruits use computed methods
    const filteredFruits = computed(() => {
      //need to get fruits.value from ref first then fileter
      return fruits.value.filter((fruit) => fruit.includes(search.value));
    });
    //use watch depends on search value changes
    const stopWatch = watch(search, () => {
      console.log("watch function runs when the serach value");
    });
    //use watchEffect will run first and depends on search value changes
    const stopWatchEffect = watchEffect(() => {
      console.log(
        "watchEffect function runs first time and runs again when the serach value",
        search.value
      );
    });
    //this function is to stop watch
    const callStopWatchFun = () => {
      stopWatch();
      stopWatchEffect();
    };
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
      search,
      fruits,
      filteredFruits,
      callStopWatchFun,
      posts,
      showPost,
      deletePost,
    };
  },
};
</script>
