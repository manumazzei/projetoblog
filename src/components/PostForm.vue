<script>
export default {
  props: {
    post: Object,
  },
  data() {
    return {
      formData: {
        title:
          this.post?.title ||
          "" /* || significa ou, se ele nao consegue um faz o outro */,
        content: this.post?.content || "",
      },
    };
  },
  methods: {
    handleCreatePost(event) {
      if (!this.formData.title) {
        alert("Preencha o título do post!");
        return;
      }

      /* adicionar o post a lista de posts */
      const now = new Date();

      const dataDaPostagem = `${now.getDate()}/${
        now.getMonth() + 1
      }/${now.getFullYear()}`;

      /*  this.posts.push({
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      });  */

      const newPost = {
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      };

      /* emitir o evento create-post */
      this.$emit("create-post", newPost);

      this.formData = {
        name: "",
        content: "",
      };
      this.$router.push("/");
    },
  },
};
</script>

<template>
  <!--   {{ formData.viewsCount }} -->
  <form>
    <input v-model="formData.title" placeholder="Titulo" />
    <textarea
      v-model="formData.content"
      placeholder="Escreva seu post aqui..."
      cols="30"
      rows="10"
    ></textarea>

    <button class="search3" type="button" @click="handleCreatePost">
      Salvar
    </button>
  </form>
</template>
