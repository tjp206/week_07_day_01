<template>
  <div id="app">
    <h1>ToDo's</h1>
    <form v-on:submit.prevent="saveNewItem">
      <label for="new-item">New to-do:</label>
      <input type="text" id="new-item" v-model="newItem.name">
      <label for="radio" v-on:click="isHighPriority(index)">High</label>
      <input type="radio" :value="true" name="radio-button" id="radio-high" v-model="newItem.isHighPriority">
      <label for="radio">Low</label>
      <input type="radio" :value="false" name="radio-button" id="radio-low" v-model="newItem.isHighPriority">
      <input type="submit" value="Save New Item">
    </form>

    <ul>
      <li v-for="(item, index) in items" v-bind:class="item.isHighPriority ? 'high-priority' : 'not-priority'" :key="index">
        <span>{{ item.name }}</span>
        </li> 
    </ul>  

  </div>
</template>

<script>
export default {
  data(){
    return {
      items: [
        {name: 'Mop the floor', isHighPriority: false},
        {name: 'Wash the clothes', isHighPriority: true},
        {name: 'Make dinner', isHighPriority: false},
      ],
      newItem: {
          name: '',
          isHighPriority: '',
      },
    };
  },
  methods: {
    saveNewItem: function () {
        this.items.push({
          name: this.newItem.name, 
          isHighPriority: this.newItem.isHighPriority,
        });
        this.newItem = {
          name: '',
          isHighPriority: '',
        }
      },
      doneItem: function (index) {
        this.items[index].isHighPriority = true;
      },
      deleteItem: function (index) {
        this.items.splice(index, 1);
      },
    },
  };
</script>

<style>
#app {
  width: 60%;
  margin: 0 auto;
  font-family: 'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

li {
  margin: 20px 0;
  padding: 10px;
  display: flex;
  justify-content: space-between;
}

li span {
  padding: 8px;
}

li button {
  background: #f2360c;
  color: #fff;
  border: none;
  padding: 10px;
  cursor: pointer;
}

li.not-priority {
  border: 4px solid #1a681e;
  color: #1a681e;
}

li.high-priority {
  border: 4px solid #f2360c;
}

input[type="text"] {
  padding: 10px;
  width: 50%;
  margin:5px;
}

button, input[type="submit"]{
  padding: 10px;
  background: #000;
  color: #fff;
  cursor: pointer;
  border: 1px solid #000;
}
</style>
