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
    width:60%;
    height: auto;
    display: flex;
    text-align: center;
    margin-left: 20%;
    margin-top: 2%;
    font-size: 25px;
} 

h2 {
  display: flex;
  justify-content: center;
  text-align: center;
  font-size: 40px;
  margin-top: 1%;
}

h4 {
  display: flex;
  justify-content: center;
  text-align: center;
}

</style>
