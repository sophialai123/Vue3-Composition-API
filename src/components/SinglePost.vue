<template>
  <div>
    <h4>{{ post.title }}</h4>
    <p>{{ snippet }}</p>
  </div>
</template>

<script>
import { computed } from "@vue/runtime-core";
export default {
  //get props from parent PostList component
  props: ["post"],

  //use props inside of setup
  setup(props) {
    //create snippet
    const snippet = computed(() => {
      //only render first 50 chracters
      return props.post.body.substring(0, 50) + "....";
    });

    //return the values to use in template
    return {
      snippet,
    };
  },
};
</script>




