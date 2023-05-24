<script>
import { RouterLink } from "vue-router";

export default {
  props: {
    posts: Array,
  },
  data() {
    return {
      search: "",
      showModal: false,
      selectedPost: null,
    };
  },
  computed: {
    filteredPosts() {
      /* 
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
    getPostId(title) {
      /* passa pela lista de posts(nao filtrada) */
      for (const index in this.posts) {
        /* acessa o post na posição index da lista de posts */
        const post = this.posts[index];
        /* verifica se o titulo do post atual é igual ao titulo buscado */
        if (post.title === title) return index;
      }
    },
    setupModal(id) {
      this.showModal = !this.showModal;
      if (id) {
        this.selectedPost = this.posts[id]; //salva o post inteiro
        return;
      }

      this.selectedPost = null;
    },
    deletePost() {
     const id =  this.getPostId(this.selectedPost.title);
     this.$emit("delete-post", id);
     this.setupModal(); //feche o modal e deselecione o post
    },
  },
};
</script>

<template>
  <div class="alinhar">
    <input
      class="search"
      v-model="search"
      placeholder="Procure pelo título do post..."/>
      <div class="feed" v-for="post in filteredPosts" :key="post.key">
        <div class="teste">
      <RouterLink :to="`/detail/${getPostId(post.title)}`">
        <h3 class="title">
          {{ post.title }}
        </h3>
      </RouterLink>
      <RouterLink :to="`/edit/${getPostId(post.title)}`">
          <span class="material-symbols-rounded">edit</span>
      </RouterLink>
          <span class="material-symbols-rounded" @click="setupModal(getPostId(post.title))">delete</span>
      <p>{{ post.content }}</p>
      <h4>{{ post.datetime }}</h4>
      </div>
    </div>
  </div>
  <div class="modal" v-show="showModal">
    <div class="modal-content">
      <h3 class="delete">Deletar Post</h3>
      <p class="sure">Tem certeza que quer deletar o post '{{ selectedPost?.title }}'?</p>

      <div class="modal-actions">
        <button class="bg-error" @click="setupModal">Cancelar</button>
        <button class="bg-success" @click="deletePost" >Confirmar</button>
      </div>
    </div>
  </div>
</template>

<style scoped>


</style>
