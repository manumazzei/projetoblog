<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/base.css";

export default {
  data() {
    return {
      posts: [],
    };
  },
  methods: {
    addPost(newPost){
     /*  adicionar o novo post a lista de posts */
      this.posts.push(newPost);
    },
  },
};
</script>

<template>
 <RouterLink to="/">Home</RouterLink>
 <RouterLink to="/create">Novo Post</RouterLink>

  <RouterView :posts="posts" @create-post="addPost"/>
</template>



<style scoped>


form {
  display: flex;
  flex-direction: column;
  text-align: center;
  justify-content: center;
  align-items: center;
}

form > * {
  margin: 1rem;
  width: 40%; 
  justify-content: center;
  border: 2px solid #35030B; 
}

.feed {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #ffe8e9; 
  color: #35030B;
  width: 100%;
  height: 70vh;
  padding-top: 0;
}

.search {
  display: flex;
  width: 40%;
  background: white;
  border: 2px solid #35030B;
  border-radius: 1ch;
  padding-top: 0;
}

.search2 {
  display: flex;
  width: 100%;
  background: #FBEEEE;
 
}

.search3{
  width: 10%;
  border-radius: 3ch;
}
.search3:hover{
  background: #35030B;
  color: #ffe8e9;
  border-radius: 3ch;
}

.post {
  border: 2px solid white;
  margin: 1rem;
  height: 200px;
  width: 300px;
  justify-content: center;
  text-align: center;
}
</style>
