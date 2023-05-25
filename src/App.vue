<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/base.css";

export default {
  data() {
    return {
      posts: [
        {
          title: "Livro - Verity",
          datetime: "18/05/2023 - 10:11:29",
          content: "Li esse livro em dois dias, a história é muito interessante, até agora não sei em quem acreditar!!! Time Carta ou Manuscrito?"
        },
        {
          title: "Livro - Uma Segunda Chance",
          datetime: "18/05/2023 - 12:23:43",
          content: "Uma história muito bonita, me emocionei do início ao fim! Vale muito a pena :)"
        },
        {
          title: "Livro - Até o Verão Terminar",
          datetime: "19/05/2023 - 15:45:22",
          content: "Um livro super fofo que te faz torcer pelos personagens o tempo inteiro, você não descansa até chegar ao fim!"
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

    <img src="https://www.imagensanimadas.com/data/media/53/livro-imagem-animada-0018.gif" class="gif">
  </main>
</template>

<style scoped>


</style>
