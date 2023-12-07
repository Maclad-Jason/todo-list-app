<template>
    <div class="todo-list">
    <img alt="Vue logo" width="50" src="../assets/logo.png">
      <h2>ToDo List Using Vue</h2>
  
      <div class="filters">
        <label>
          <input type="radio" v-model="filter" value="all">
          All
        </label>
        <label>
          <input type="radio" v-model="filter" value="completed">
          Completed
        </label>
        <label>
          <input type="radio" v-model="filter" value="incomplete">
          Incomplete
        </label>
      </div>
  
      <ul class="items">
        <li v-for="item in filteredItems" :key="item.id">
          <input type="checkbox" v-model="item.completed">
          <span class="item-text" :class="{ completed: item.completed }">{{ item.text }}</span>
          <button class="delete-btn" @click="removeItem(item)">Delete</button>
        </li>
      </ul>
  
      <form class="add-item-form" @submit.prevent="addItem">
        <input type="text" v-model="newItem" placeholder="Add a new item">
        <button class="add-btn">Add</button>
      </form>
    </div>
  </template>
  
<script>
export default {
    data() {
        return {
            items: [
                { id: 1, text: 'Learn Vue.js', completed: false },
                { id: 2, text: 'Build an app', completed: false },
                { id: 3, text: 'Deploy the app', completed: false },
            ],
            newItem: '',
            filter: 'all'
        };
    },
    methods: {
        addItem() {
            if (this.newItem.trim()) {
                this.items.push({
                    id: this.items.length + 1,
                    text: this.newItem.trim(),
                    completed: false
                });
                this.newItem = '';
            }
        },
        removeItem(item) {
            const index = this.items.indexOf(item);
            this.items.splice(index, 1);
        }
    },
    computed: {
        filteredItems() {
            switch (this.filter) {
                case 'completed':
                    return this.items.filter(item => item.completed);
                case 'incomplete':
                    return this.items.filter(item => !item.completed);
                default:
                    return this.items;
            }
        }
    }
};
</script>

