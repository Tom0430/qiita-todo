<template>
  <v-form>
    <v-container>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field v-model="title" :counter="10" label="todo" required @keydown.enter.exact.prevent="handleSubmit"></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-btn @click.prevent="handleSubmit">作成</v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>
<script>
export default {
  data() {
    return {
      title: ""
    };
  },
   methods: {
    handleSubmit() {
      const todo = {
        title: this.title,
        user_id: this.$store.state.currentUser.id,
      };
      this.$emit("submit", todo);
      this.title = "";
    }
  }
};
</script>

<style>
</style>