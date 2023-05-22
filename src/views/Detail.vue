<script>
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
};

</script>

<template>
<h2>{{ post.title }}</h2>
<h4>{{ post.datetime }}</h4>

<textarea readonly :value="post.content"></textarea>
</template>

<style scoped>
textarea {
    resize: none;
    outline: none;
    border: none;
    width:80%;

}
</style>
