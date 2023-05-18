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
      ],
    };
  },
  methods: {
    addPost(newPost) {
      /*  adicionar o novo post a lista de posts */
      this.posts.push(newPost);
    },
    updatePost(updatedPost, id) {
        this.posts[id] = updatedPost;
    },
  },
};
</script>

<template>
  <header>
    <nav>
      <RouterLink to="/" class="link">Home</RouterLink>
      <RouterLink to="/create" class="link">Novo Post</RouterLink>
    </nav>
  </header>
  <main>
    <RouterView :posts="posts" @create-post="addPost" @edit-post="updatePost"/>
  </main>
</template>

<style scoped>

.link{
 width: 25%;
 height: 40px;
 border: 2px solid #35030b;
 justify-content: center;
 text-align: center;
 border-radius: 3ch;
 background: whitesmoke;
 color:#35030b;
 text-decoration: none;
 font-family: fantasy;
}

.link:hover{
  background: #35030b;
  color: #ffe8e9;
  border-radius: 3ch;
}
</style>
