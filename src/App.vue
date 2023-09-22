<script setup>
  import { ref } from 'vue'
  const list = ref([
    'Buy an apple watch',
    'Buy a Macbook'
  ])
  let edit = ref(false)
  const showForm = () => {
    edit.value = true
  }
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
          <div @click="showForm" class="add">+</div>
        </div>
      </div>
      <div class="body">
        <form @submit.prevent="addItem" v-if="edit">
          <input
            type="text"
            v-model.trim="newTask"
            placeholder="Type and press enter"
          >
          <button type="submit">Add</button>
        </form>
        <ul>
          <li v-for="item in list" :key="item.id" v-text="item" />
      </ul>
      </div>
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
    min-width: 350px;
    display: flex;
    flex-direction: column;
    gap: 0.075em;
    .header {
      background: white;
      padding: 1.5em 1.5em 0.65em;
      border-radius: 1em 1em 0 0;
      font-size: 1.2em;
      display: flex;
      justify-content: space-between;
      .actions {
        .add {
          cursor: pointer;
        }
      }
    }

    .body {
      background: white;
      padding: 0.75em 1.5em 1.5em;
      border-radius: 0 0 1em 1em;
      form {
        padding: 1em 0 0.5em;
        display: flex;
        gap: 0.25em;
        justify-content: space-between;
        input {
          outline: none;
          border: none;
          border-bottom: 1px solid rgba(44, 53, 57, 0.5);
          padding: 0.25em 0em;
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
        margin-top: 0.5em;
        list-style: none;
        li {
          color: rgba(44, 53, 57, 0.75)
        }
      }
    }
  }
}
</style>
