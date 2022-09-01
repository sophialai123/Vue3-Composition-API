<template>
  <h1>This is Post List Component</h1>
  <div v-for="post in posts" :key="post.id">
    <!--   Post Title: {{ post.title }} -->

    <!-- render singlepos component and pass post 
    as a props-->
    <SinglePost :post="post" />
  </div>
</template>

<script>
import { onMounted, onUnmounted, onUpdated } from "@vue/runtime-core";
import SinglePost from "./SinglePost.vue";
export default {
  //pass pros as a props data here
  props: ["posts"],
  //use props inside of setup function
  setup(props) {
    //use lifehooks inside of setup function
    //callback function component has been mounted
    onMounted(() => console.log("on mounted")),
      onUnmounted(() => console.log("un mounted")),
      onUpdated(() => console.log("updated mounted "));
    //get value from posts
    console.log(props.posts);
  },
  components: { SinglePost },
};
</script>


<style>
</style>
