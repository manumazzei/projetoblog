<script>
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu Primeiro Post",
          datetime: Date.now(),
          content: "Postar aqui é muito legal",
        },

        {
          title: "Meu Segundo Post",
          datetime: Date.now(),
          content: "Postar aqui não é muito legal",
        },
      ],
      formData: {
        title: "",
        content: "",
      },
      search: "",
    };
  },
  computed: {
    filteredPosts() {/* 
      se search estiver vazia, retorne a lista completa de posts */
      if (!this.search) return this.posts;

    /*   se tiver qualquer coisa em this.search, faz o filtro */
      const listaFiltrada = [];

      for (const post of this.posts) {
        if (this.search && post.title.includes(this.search)) {
          listaFiltrada.push(post);
        }
      }
      return listaFiltrada;
    },
  },
  methods: {
    handleClick(event) {
      /* adicionar o post a lista de posts */
      const now = new Date()

      const dataDaPostagem = `${now.getDate()}/${now.getMonth()+1}/${now.getFullYear()}`;

      this.posts.push({
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      });

      this.formData = {
        name:"",
        content: "",
      };
    },
    handleImputChange(event) {
      const { name, value } = event.target;
      this.formData[name] = value;
    },
  },
};
</script>

<template>
  
  <div class="feed">
    <input class="search" v-model="search" placeholder="Procure pelo título do post..."/> 
    <div class="post" v-for="post in filteredPosts" :key="post.key"> 
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>

  <form class="search2">
    <input class="search" v-model="formData.title" placeholder="Titulo"/>
    <textarea class="search"
      name="content"
      :value="formData.content"
      @keyup="handleImputChange"
      placeholder="Escreva seu post aqui..."
      id="lista-posts"
      cols="30"
      rows="10"
    ></textarea>

    <button class="search3" type="button" @click="handleClick">Salvar</button>
  </form>
  <RouterView />
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
