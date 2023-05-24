<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/base.css";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro Post",
          datetime: "18/5/2023",
          content: "Conteudo magnifico"
        },
        {
          title: "Meu segundo Post",
          datetime: "18/5/2023",
          content: "Conteudo magnifico"
        },
        {
          title: "Meu terceiro Post",
          datetime: "18/5/2023",
          content: "Conteudo magnifico"
        },
      ],
    };
  },
  methods: {
    addPost(newPost) {
      /*  adicionar o novo post a lista de posts */
      this.posts.push(newPost);
    },
    updatePost(updatedPost, id) {
      this.posts [id] = updatedPost;
    },
    removePost(id) {
      const minhaNovaLista = [];

      for(const index in this.posts) {
        if(index ==id) {
          continue;
        }
        const post = this.posts [index];
        minhaNovaLista.push(post);
      }
      this.posts = minhaNovaLista;
    },
  },
};
</script>

<template>
  <header>
    <nav>
      <RouterLink to="/" class="botao">Home</RouterLink>
      <img src="/text-books.png">
      <RouterLink to="/create" class="botao">Novo Post</RouterLink>
    </nav>
  </header>
  <main>
    <RouterView :posts="posts" 
    @create-post="addPost" 
    @edit-post="updatePost" 
    @delete-post="removePost"/>
  </main>
</template>

<style scoped>


</style>
