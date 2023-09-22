<script setup>
  import { ref } from 'vue'
  const list = ref([
    {id: 1, completed: true, title: 'Suddenly I saw you'},
    {id: 2, completed: false, title: 'Immediately I chose you'},
    {id: 3, completed: false, title: 'Then arranged to meet you'},
    {id: 4, completed: true, title: 'The result was confused'},
    {id: 5, completed: false, title: 'But, I failed to forget you'}
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
    if(newTask.value !== '') {
      list.value.push({
        id: list.value.length + 1, completed: false, title: newTask.value
      })
    }
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
        <div class="title">{{ list.length }} steps of my Life</div>
      </div>
      <div class="body">

        <ul>
            <li v-for="item in list" :key="item.id" @click="toggleCompletion(item)" :class="{ completed : item.completed}"><input :checked="item.completed" type="radio">{{ item.title }}</li>
        </ul>

        <button @click="showForm" class="add">+</button>

      </div>
    </div>

    <div class="new_item_card" v-if="edit">
      <div class="body">
        <form @submit.prevent.enter="addItem">
          <input
            type="text"
            v-model.trim.toUpperCase="newTask"
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
  background: rgba(240,244,211,1);
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
    box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px;
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
          align-items: center;
          gap: 0.25rem;
          color: rgba(44, 53, 57, 0.65);
          transition: all 0.5s ease-in;
          input[type='radio'] {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 1rem;
            height: 1rem;
            border-radius: 50%;
            border: 0.0025rem solid gray;
          }
          input[type='radio']:focus,
          input[type='radio']:checked {
           appearance: none;
           border: 0.0025rem solid rgba(44, 53, 57, 0.25);
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
        transition: 0.5s;
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
    box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px;
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
      transition: 0.5s;
    }
    .cross:hover {
      cursor: pointer;
      background: rgb(226, 6, 112);
    }
  }
}
</style>
