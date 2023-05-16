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
    };
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
  <div id="lista-posts">
    <div v-for="post in posts" :key="post.key">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>

  <form>
    <input v-model="formData.title" placeholder="Titulo"/>
    <textarea
      name="content"
      :value="formData.content"
      @keyup="handleImputChange"
      placeholder="Escreva seu post aqui..."
      id=""
      cols="30"
      rows="10"
    ></textarea>

    <button type="button" @click="handleClick">Salvar</button>
  </form>

  <RouterView />
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  border: 2px solid #35030B;
  width: 50%;
  align-items: center;
}

form > * {
  margin: 1rem;
  width: 60%;
}

#lista-posts {
  background: #ECDCCE;
  color: #35030B;
  padding: 2rem 2rem;
  font-family: Impact;
}

</style>
