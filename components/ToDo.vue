
<template>
  <div id="bulb-section">
    <form class="form-bulb" v-on:submit.prevent="addNewBulb">
      <div class="form-item">
        <label for="new-room">команата</label>
        <select v-model="selected">
          <option disabled value="Выберите комнату">Выберите комнату</option>
          <option>Кухня</option>
          <option>Зал</option>
          <option>Спальня</option>
        </select>
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

    <div class="content-section">
      <ul>
        <li class=""
          v-for="(todo) in todos"
          v-bind:key="todo.id"
          v-bind:class="todo.addClass">
          <span>
            {{ todo.id }}
          </span>
          <span>
            {{ todo.titleRoom }}
          </span>
          </li>
      </ul>
<!--  Kitchen-->
      <table>
        <tr>
          <th>команата</th>
          <th>расположение лампочки</th>
          <th>дата установки</th>
          <th>гарантия до</th>
          <th></th>
        </tr>
        <tr v-for="(todo) in arrayKitchen"
        v-bind:key="todo.id"
        v-bind:title="todo.titleRoom" class="kitchen">
          <td>
            {{ todo.id }}
              Кухня
          </td>
          <td>
              {{ todo.titlePosition }}
          </td>
          <td>
              {{ todo.titleDate }}
          </td>
          <td>
              {{ todo.titleGaranty }}
          </td>
          <td>
            <button v-on:click="removeArrayKitchen()">Удалить</button>
          </td>
        </tr>
      </table>
<!--  Guest -->
      <table style="color: red">
        <tr>
          <th>команата</th>
          <th>расположение лампочки</th>
          <th>дата установки</th>
          <th>гарантия до</th>
          <th></th>
        </tr>
        <tr v-for="(todo) in arrayGuest"
        v-bind:key="todo.id"
        v-bind:title="todo.titleRoom" class="guest">
          <td>
            {{ todo.id }}
              Зал
          </td>
          <td>
              {{ todo.titlePosition }}
          </td>
          <td>
              {{ todo.titleDate }}
          </td>
          <td>
              {{ todo.titleGaranty }}
          </td>
          <td>
            <button v-on:click="removeTodo()">Удалить</button>
          </td>
        </tr>
      </table>
<!--  Bedroom-->
      <table style="color: green">
        <tr>
          <th>команата</th>
          <th>расположение лампочки</th>
          <th>дата установки</th>
          <th>гарантия до</th>
          <th></th>
        </tr>
        <tr v-for="(todo) in arrayBedroom"
        v-bind:key="todo.id"
        v-bind:title="todo.titleRoom" class="bedroom">
          <td>
            {{ todo.id }}
              Спальня
          </td>
          <td>
              {{ todo.titlePosition }}
          </td>
          <td>
              {{ todo.titleDate }}
          </td>
          <td>
              {{ todo.titleGaranty }}
          </td>
          <td>
            <button v-on:click="removeTodo()">Удалить</button>
          </td>
        </tr>
      </table>

    </div>
    <div class="item-room" id="kitchen">
      <div class=""
      v-for="(todo) in arrayKitchen"
      v-bind:key="todo.id"
      v-bind:class="todo.itemBulb"></div>

    </div>
    <div class="item-room" id="guest">
      <div class=""
      v-for="(todo) in arrayGuest"
      v-bind:key="todo.id"
      v-bind:class="todo.itemBulb"></div>
    </div>
    <div class="item-room" id="bedroom">
      <div class=""
      v-for="(todo) in arrayBedroom"
      v-bind:key="todo.id"
      v-bind:class="todo.itemBulb"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ToDo',
  data () {
    return {
      selected: '',
      newRoom: '',
      newDate: '',
      newPosition: '',
      newGaranty: '',
      todos: [ ],
      nextIdKitchen: 1,
      nextIdGuest: 1,
      nextIdBedroom: 1,
      showRoom: false,
      rooms: [],
      arrayKitchen: [],
      arrayGuest: [],
      arrayBedroom: [],
      nextItemId: 1,
      showRoomClass: 'item-room show',
      newRoomName: '',
      itemBulb: 'item-bulb'
    }
  },
  mounted() {
    if (localStorage.getItem('arrayKitchen')) {
      try {
        this.arrayKitchen = JSON.parse(localStorage.getItem('arrayKitchen'));
      } catch(e) {
        localStorage.removeItem('arrayKitchen');
      }
    } else if (localStorage.getItem('arrayGuest')) {
      try {
        this.arrayGuest = JSON.parse(localStorage.getItem('arrayGuest'));
      } catch(e) {
        localStorage.removeItem('arrayGuest');
      }
    } else if (localStorage.getItem('arrayBedroom')) {
      try {
        this.arrayBedroom = JSON.parse(localStorage.getItem('arrayBedroom'));
      } catch(e) {
        localStorage.removeItem('arrayBedroom');
      }
    }
  },
  methods: {
    addNewBulb: function () {
      if (this.selected === 'Кухня') {
        this.arrayKitchen.push({
          itemBulb: this.itemBulb,
          id: this.nextIdKitchen++,
          titleRoom: this.newRoom,
          titlePosition: this.newPosition,
          titleDate: this.newDate,
          titleGaranty: this.newGaranty
        })
      } else if (this.selected === 'Зал'){
        this.arrayGuest.push({
          itemBulb: this.itemBulb,
          id: this.nextIdGuest++,
          titleRoom: this.newRoom,
          titlePosition: this.newPosition,
          titleDate: this.newDate,
          titleGaranty: this.newGaranty
        })
      } else if (this.selected === 'Спальня'){
        this.arrayBedroom.push({
          itemBulb: this.itemBulb,
          id: this.nextIdBedroom++,
          titleRoom: this.newRoom,
          titlePosition: this.newPosition,
          titleDate: this.newDate,
          titleGaranty: this.newGaranty
        })
      }
      this.saveArrayGuest();
      this.saveArrayKitchen();

      //this.newRoom = ''
    },
    removeArrayKitchen(x) {
      this.arrayKitchen.splice(x, 1);
      this.saveArrayKitchen();
    },
    removeArrayGuest(x) {
      this.arrayGuest.splice(x, 1);
      this.saveArrayGuest();
    },
    saveArrayKitchen() {
      const parsed = JSON.stringify(this.arrayKitchen);
      localStorage.setItem('arrayKitchen', parsed);
    },
    saveArrayGuest() {
      const parsed = JSON.stringify(this.arrayGuest);
      localStorage.setItem('arrayGuest', parsed);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#bulb-section{
  display: flex;
  justify-content: space-between;
}
.form-bulb{
  width: 330px;
  margin-top: 20px;
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
  width: 600px;
}
li {
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
  text-align: left;
}
.add-room{
  display: inline-block;
  padding: 5px 15px;
  margin-bottom: 15px;
  text-transform: uppercase;
  border: 1px solid red;
  cursor: pointer;
}
.item-room{
  width: 100px;
  height: 100px;
  background-color: rgba(0, 0, 0, 0.2);
  border: 1px solid green;
}
table{
  width: 700px;
  border: 1px solid grey;
  border-collapse: collapse
}
td, th{
  text-align: center;
  border: solid 1px #ccc;
}
th:last-child{
  width: 87px;
}
.item-bulb{
  display: inline-block;
  width: 5px;
  height: 5px;
  background: aqua;
  margin: 5px;
}

</style>
