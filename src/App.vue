<template>
  <div>
    <h1>My To-Do List</h1>
    <div class="input-container">
      <input type="text" v-model="newItem" placeholder="Add new item">
      <button @click="addItem">Add</button>
    </div>
    <div>
      <input type="checkbox" id="show-completed" v-model="showCompleted">
      <label for="show-completed">Show completed items only</label>
    </div>
    <ul>
      <li v-for="(item, index) in filteredItems" :key="index" :class="{ completed: item.completed }">
        <div class="item-container">
          <input type="checkbox" v-model="item.completed" @change="toggleCompleted(index)">
          <span v-if="!item.completed">{{ item.text }}</span>
          <s v-else>{{ item.text }}</s>
          <button class="remove-button" @click="removeItem(index)">Remove</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      items: [],
      newItem: '',
      showCompleted: false
    }
  },
  computed: {
    filteredItems() {
      if (this.showCompleted) {
        return this.items.filter(item => item.completed)
      } else {
        return this.items.filter(item => !item.completed)
      }
    }
  },
  methods: {
    addItem() {
      if (this.newItem !== '') {
        this.items.push({
          text: this.newItem,
          completed: false
        })
        this.newItem = ''
      }
    },
    removeItem(index) {
      this.items.splice(index, 1)
    },
    toggleCompleted(index) {
      this.items[index].completed = !this.items[index].completed
    }
  }
}
</script>

<style>
h1 {
  text-align: center;
  font-size: 36px;
  margin-bottom: 30px;
}

.input-container {
  display: flex;
  margin-bottom: 20px;
}

input[type="text"] {
  flex-grow: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  margin-right: 10px;
}

button {
  background-color: #ccc
}