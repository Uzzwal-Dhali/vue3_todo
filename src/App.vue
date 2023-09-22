<script setup>
  import { ref } from 'vue'
  const list = ref([
    {id: 1, completed: true, title: 'Learn HTML & CSS'},
    {id: 2, completed: false, title: 'Dive into JavaScript'},
    {id: 3, completed: false, title: 'Learn PHP'},
    {id: 4, completed: true, title: 'Start Laravel & make a project'},
    {id: 5, completed: false, title: 'Design with VueJS'}
  ])
  let edit = ref(false)
  const showForm = () => {
    edit.value = true
  }

  const closeForm = () => {
    edit.value = false
  }

  const newTask = ref('')
  const addItem = () => {
    list.value.push({
      completed: false, title: newTask.value
    })
    newTask.value = ''
  }

  const toggleCompletion = (item) => {
    item.completed = !item.completed
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
            <li v-for="item in list" :key="item.id" @click="toggleCompletion(item)" :class="{ completed : item.completed}"><input :checked="item.completed" type="radio"> {{ item.title }}</li>
        </ul>

        <button @click="showForm" class="add">+</button>

      </div>
    </div>

    <div class="new_item_card" v-if="edit">
      <div class="body">
        <form @submit.prevent="addItem">
          <input
            type="text"
            v-model.trim="newTask"
            placeholder="Type and press enter"
          >
        </form>
      </div>
      <div class="cross" @click="closeForm">+</div>
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
    padding: 2.2em 1.8rem 3rem;
    border-radius: 0.75rem;
    min-width: 330px;
    display: flex;
    flex-direction: column;
    gap: 0.005em;
    .header {
      font-size: 1.2em;
      display: flex;
      justify-content: space-between;
      padding: 0.5rem 0 0.5rem;
      .title {
        font-size: 1em;
        /* color: rgba(44, 53, 57, 0.75); */
        color: rgb(15, 143, 152);
      }

    }
    .body {

      ul {
        margin-top: 0.5em;
        list-style: none;
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
        li {
          cursor: pointer;
          display: flex;
          gap: 0.25rem;
          color: rgba(44, 53, 57, 0.65);
          transition: all 0.5s ease-in;
          input[type='checkbox'] {
            border-radius: 50%;
          }
        }
        li:hover {
          cursor: pointer;
        }
        .completed {
          color: rgba(44, 53, 57, 0.25);
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
        background: rgba(15, 143, 152, 0.8);
        border: none;
        color: white;
        font-size: 1.7rem;
        left: 50%;
        transform: translateX(-50%) translateY(50%);
      }
      .add:hover {
        background: rgba(15, 143, 152, 1);
      }
    }
  }
  .new_item_card {
    background: white;
    padding: 1.5rem 1.8rem;
    border-radius: 0.75rem;
    min-width: 330px;
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
    }
    .cross {
      position: absolute;
      width: 50px;
      height: 50px;
      background: rgba(226, 6, 112, 0.8);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-size: 1.7rem;
      left: 50%;
      transform: translateX(-50%) translateY(5%) rotate(45deg);
    }
    .cross:hover {
      cursor: pointer;
      background: rgb(226, 6, 112);
    }
  }
}
</style>
