<script setup>
  import { ref } from 'vue'
  const list = ref([
    'Buy an apple watch',
    'Buy a Macbokk'
  ])
  const newTask = ref('')
  const addItem = () => {
    list.value.push(newTask.value)
    newTask.value = ''
  }
</script>

<template>
  <div class="container">
    <div class="card">
      <div class="header">
        <div class="title">Things to do</div>
        <div class="actions">
          <div class="add">+</div>
        </div>
      </div>
      <form @submit.prevent="addItem">
        <input type="text" v-model.trim="newTask">
        <button type="submit">Add</button>
      </form>
      <ul>
        <li v-for="item in list" :key="item.id" v-text="item" />
      </ul>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.container {
  background: #36454F;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  .card {
    background: white;
    padding: 1.5em;
    border-radius: 1em;
    .header {
      font-size: 1.2em;
      border-bottom: 1px solid rgba(0, 0, 0, 0.25);
      display: flex;
      justify-content: space-between;
      .actions {
        .add {
          cursor: pointer;
        }
      }
    }
    form {
      padding: 1em 0;
      display: flex;
      gap: 0.25em;
      input {
        border-radius: 0.25em;
        outline: none;
        border: 1px solid rgba(44, 53, 57, 0.5);
        padding: 0.25em 0.75em;
      }
      button {
        background: rgb(15, 143, 152);
        border-radius: 0.35em;
        border: none;
        color: white;
        padding: 0.3em 0.75em;
      }
    }
    ul {
      list-style: none;
      li {
        color: rgba(44, 53, 57, 0.75)
      }
    }
  }
}
</style>
