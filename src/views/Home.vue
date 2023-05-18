<script>
export default {
  props:{
    posts: Array,
  },
  data () {
    return {
      search:"",
    }
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
};
</script>

<template>
  <div class="alinhar">
    <input class="search" v-model="search" placeholder="Procure pelo título do post..." /> 
    <div class="feed" v-for="post in filteredPosts" :key="post.key">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div> 
</template>

<style scoped>
.alinhar{
  display: flex;
  justify-content: center;
  align-items:first baseline;
  padding-top: 2rem;
  background: #ffe8e9;
  height: 73vh;
}

.feed{
  border: 2px solid black;
  flex-direction: column;
}
</style>