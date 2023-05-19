<script>

import PostForm from "@/components/PostForm.vue";

export default {
  props: {
    posts: Array,
  },
  data() {
   // acessa o parametro id apenas uma vez
    const id = this.$route.params.id;
    return {
      id: id, //expondo a variavel id para ser acessivel no template
      post: this.posts[id],
    };
  },
  components: {
    PostForm,
  },
};

</script>

<template>
    <PostForm :post="post" :id="id" />
</template>
