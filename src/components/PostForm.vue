<script>
export default {
  props: {
    post: Object,
    id: String,
  },
  data() {
    return {
      formData: {
        title:
          this.post?.title ||
          "" /* || significa ou, se ele nao consegue um faz o outro */,
        content: this.post?.content || "",
      },
      isEditing: Boolean(this.post),
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
      }/${now.getFullYear()} - ${now.getHours()}:${now.getMinutes()}:${now.getSeconds()}`;

      /*  this.posts.push({
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      });  */

      const postData = {
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      };

      if (this.isEditing) {
        this.$emit("edit-post", postData, this.id);
      } else {
        this.$emit("create-post", postData);
      };

      /* this.formData = {
        name: "",
        content: "",
      };
      this.$router.push("/"); */

      this.$router.push("/");
    },
  },
};
</script>

<template>
  <form>
    <input v-model="formData.title" placeholder="Titulo" />
    <textarea
      v-model="formData.content"
      placeholder="Escreva seu post aqui..."
      cols="30"
      rows="10"
    ></textarea>

    <button class="create" type="button" @click="handleCreatePost">
      Salvar
    </button>
  </form>
</template>
