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
        <div class="title">{{ list.length }} Things to do</div>
      </div>
      <div class="body">

        <ul>
          <li v-for="item in list" :key="item.id" v-text="item" />
        </ul>

        <button @click="showForm" class="add">+</button>

      </div>
    </div>

    <div class="card" v-if="edit">
      <div class="body">
        <form @submit.prevent="addItem">
          <input
            type="text"
            v-model.trim="newTask"
            placeholder="Type and press enter"
          >
          <!-- <button type="submit">Add</button> -->
        </form>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.container {
  background: #36454F;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 2.5em;
  .card {
    background: white;
    padding: 1.5em;
    border-radius: 0.75rem;
    min-width: 350px;
    display: flex;
    flex-direction: column;
    gap: 0.005em;
    .header {
      font-size: 1.2em;
      display: flex;
      justify-content: space-between;
      .title {
        font-size: 1em;
        color: rgba(44, 53, 57, 0.75);
      }

    }

    .body {
      form {
        padding: 0.75em 0 0.5em;
        display: flex;
        gap: 0.25em;
        justify-content: space-between;
        input {
          width: 100%;
          outline: none;
          border: none;
          border-bottom: 1px solid rgba(44, 53, 57, 0.25);
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
      .add {
        position: absolute;
        cursor: pointer;
        border-radius: 50%;
        width: 50px;
        height: 50px;
        display: flex;
        justify-content: center;
        align-items: center;
        background: rgb(15, 143, 152);
        border: none;
        color: white;
        font-size: 1.7rem;
        left: 50%;
        transform: translateX(-50%);
      }
    }
  }
}
</style>
