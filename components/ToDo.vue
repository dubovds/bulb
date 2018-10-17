<template>
  <div id="todo-list-example">
    <form class="form-bulb" v-on:submit.prevent="addNewTodo">
      <div class="form-item">
        <label for="new-room">команата</label>
        <input
          v-model="newRoom"
          id="new-room"
          placeholder="Кухня"
        >
      </div>
      <div class="form-item">
        <label for="new-position">расположение лампочки</label>
        <input
          v-model="newPosition"
          id="new-position"
          placeholder="В правом углу"
        >
      </div>
      <div class="form-item">
        <label for="new-date">дата установки</label>
        <input
          v-model="newDate"
          id="new-date"
          placeholder="12.10.2018"
        >
      </div>
      <div class="form-item">
        <label for="new-garanty">гарантия до</label>
        <input
          v-model="newGaranty"
          id="new-garanty"
          placeholder="10.2019"
        >
      </div>
      <button>Добавить</button>
    </form>
    <ul>
      <li class="item"
      v-for="(todo) in todos"
      v-bind:key="todo.id"
      v-bind:title="todo.titleRoom"
      >
        <span>
          {{ todo.id }}
          команата:
            {{ todo.titleRoom }}
        </span>
        <span>
          расположение лампочки:
            {{ todo.titlePosition }}
        </span>
        <span>
          дата установки:
            {{ todo.titleDate }}
        </span>
        <span>
          гарантия до:
            {{ todo.titleGaranty }}
        </span>
        <button v-on:click="removeTodo()">Удалить</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'ToDo',
  data () {
    return {
      msg: 'Добавить лампочку',
      newRoom: '',
      newDate: '',
      newPosition: '',
      newGaranty: '',
      todos: [

      ],
      nextTodoId: 1
    }

  },
  mounted() {
    if (localStorage.getItem('todos')) {
      try {
        this.todos = JSON.parse(localStorage.getItem('todos'));
      } catch(e) {
        localStorage.removeItem('todos');
      }
    }
  },
  methods: {
    addNewTodo: function () {
      this.todos.push({
        id: this.nextTodoId++,
        titleRoom: this.newRoom,
        titlePosition: this.newPosition,
        titleDate: this.newDate,
        titleGaranty: this.newGaranty
      }),
      this.saveTodos();
      //this.newRoom = ''
    },
    removeTodo(x) {
      this.todos.splice(x, 1);
      this.saveTodos();
    },
    saveTodos() {
      const parsed = JSON.stringify(this.todos);
      localStorage.setItem('todos', parsed);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.form-bulb{
  width: 330px;
  margin:auto;
}
.form-item{
    display: flex;
    justify-content: space-between;
    margin-bottom: 10px;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.item{
  border: 1px solid green;
  padding: 10px;
}
.item span{
  display: block;
  text-align: left;
}
</style>
