<script>
export default {
  data() {
    return {
      formData: {
        title: "",
        content: "",
      },
    };
  },
  methods: {
    handleClick(event) {

      if(!this.formData.title) {
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

      const newPost={
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
      this.$router.push("/")
    },

    handleImputChange(event) {
      const { name, value } = event.target;
      this.formData[name] = value;
    },
  },
};
</script>

<template>
  <form>
    <input v-model="formData.title" placeholder="Titulo" />
    <textarea
      name="content"
      :value="formData.content"
      @keyup="handleImputChange"
      placeholder="Escreva seu post aqui..."
      id=""
      cols="30"
      rows="10"
    ></textarea>

    <button class="search3" type="button" @click="handleClick">Salvar</button>
  </form>
</template>

<style scoped>
</style>
