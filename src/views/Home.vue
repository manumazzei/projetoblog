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
      <p>{{ post.content }}</p>
      <h4>{{ post.datetime }}</h4>
    </div>
  </div> 
</template>

<style scoped>
.alinhar{
  display: flex;
  justify-content: first baseline;
  padding-top: 2rem;
  background: #ffe8e9;
  height: 100vh;
  align-items: center;
  flex-direction: column;
}

.feed{
border: 2px solid #35030b;
margin-top: 2rem; 
display:inline-flexbox;
width: 300px;
height: 300px;
text-align: center;
border-radius: 3ch;
background: whitesmoke;
position: relative;
}

.feed:hover{
  transform: scale(1.1);
  transition: all 0.5s;
}

h3{
  font-size: 25px;
  justify-content: first baseline;
  font-family: fantasy;
}

p{
  font-size: 20px;
  font-family: monospace;
}

h4{
  font-size: 13px;
  justify-content: last baseline;
}
</style>