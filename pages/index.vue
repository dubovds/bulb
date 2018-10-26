<template>
  <section class="container">
    <div class="top">
      <div class="logo-title">
        <app-logo/>
        <h1 class="title">
          bulb
        </h1>
      </div>
      <div class="rooms-section">
        <div class="item-room" id="kitchen">
          <div class=""
          v-for="(todo) in arrayKitchen"
          v-bind:key="todo.id"
          v-bind:class="todo.itemBulb"></div>
          <span class="item-room__title">Кухня</span>

        </div>
        <div class="item-room" id="guest">
          <div class=""
          v-for="(todo) in arrayGuest"
          v-bind:key="todo.id"
          v-bind:class="todo.itemBulb"></div>
          <span class="item-room__title">Зал</span>
        </div>
        <div class="item-room" id="bedroom">
          <div class=""
          v-for="(todo) in arrayBedroom"
          v-bind:key="todo.id"
          v-bind:class="todo.itemBulb"></div>
          <span class="item-room__title">Спальня</span>
        </div>
      </div>
    </div>
      <div id="bulb-section">
        <!-- <form class="form-bulb"> -->
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
                <button v-on:click="removeKitchen()">Удалить</button>
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
                <button v-on:click="removeGuest()">Удалить</button>
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
                <button v-on:click="removeBedroom()">Удалить</button>
              </td>
            </tr>
          </table>

        </div>
      </div>
  </section>
</template>

<script>
import Vue from 'vue'
import ToDo from '~/components/ToDo.vue'
import AppLogo from '~/components/AppLogo.vue'

export default {
  components: {
    ToDo,
    AppLogo
  },
  data () {
    return {
      arrayKitchen: [],
      arrayGuest: [],
      arrayBedroom: [],
      selected: '',
      newRoom: '',
      newDate: '',
      newPosition: '',
      newGaranty: '',
      nextIdKitchen: 1,
      nextIdGuest: 1,
      nextIdBedroom: 1,
      itemBulb: 'item-bulb'
      //newRoomName: '',
      //todos: [ ],
      //showRoom: false,
      //rooms: [],
      //nextItemId: 1,
      //showRoomClass: 'item-room show',
    }
  },
  mounted() {
    if (localStorage.getItem('arrayKitchen')) {
      try {
        this.arrayKitchen = JSON.parse(localStorage.getItem('arrayKitchen'));
      } catch(e) {
        localStorage.removeItem('arrayKitchen');
      }
    };
    if (localStorage.getItem('arrayGuest')) {
      try {
        this.arrayGuest = JSON.parse(localStorage.getItem('arrayGuest'));
      } catch(e) {
        localStorage.removeItem('arrayGuest');
      }
    };
    if (localStorage.getItem('arrayBedroom')) {
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
        }),
        this.newRoom = '',
        this.newPosition = '',
        this.newDate = '',
        this.newGaranty = '',
        this.selected = '',
        this.saveArrayKitchen();
      } else if (this.selected === 'Зал'){
        this.arrayGuest.push({
          itemBulb: this.itemBulb,
          id: this.nextIdGuest++,
          titleRoom: this.newRoom,
          titlePosition: this.newPosition,
          titleDate: this.newDate,
          titleGaranty: this.newGaranty
        }),
        this.newRoom = '',
        this.newPosition = '',
        this.newDate = '',
        this.newGaranty = '',
        this.saveArrayGuest();
      } else if (this.selected === 'Спальня'){
        this.arrayBedroom.push({
          itemBulb: this.itemBulb,
          id: this.nextIdBedroom++,
          titleRoom: this.newRoom,
          titlePosition: this.newPosition,
          titleDate: this.newDate,
          titleGaranty: this.newGaranty
        }),
        this.newRoom = '',
        this.newPosition = '',
        this.newDate = '',
        this.newGaranty = '',
        this.saveArrayBedroom();
      }
    },
    removeKitchen(x) {
      this.arrayKitchen.splice(x, 1);
      this.saveArrayKitchen();
    },
    removeGuest(x) {
      this.arrayGuest.splice(x, 1);
      this.saveArrayGuest();
    },
    removeBedroom(x) {
      this.arrayBedroom.splice(x, 1);
      this.saveArrayBedroom();
    },
    saveArrayKitchen() {
      const parsed = JSON.stringify(this.arrayKitchen);
      localStorage.setItem('arrayKitchen', parsed);
    },
    saveArrayGuest() {
      const parsed = JSON.stringify(this.arrayGuest);
      localStorage.setItem('arrayGuest', parsed);
    },
    saveArrayBedroom() {
      const parsed = JSON.stringify(this.arrayBedroom);
      localStorage.setItem('arrayBedroom', parsed);
    }

  }
}

</script>

<style>
.container {
  width: 1140px;
  margin: auto;
}
.top{
  display: flex;
  justify-content: space-between;
}
.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
.add_room{
  display: inline-block;
  margin-top: 15px;
  padding: 5px 15px;
  border: 1px solid green;
  border-radius: 5px;
  cursor: pointer;
}
#bulb-section{
  display: flex;
  justify-content: space-between;
  margin-top: 20px;
}
.form-bulb{
  width: 330px;
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
table{
  width: 700px;
  border: 1px solid grey;
  border-collapse: collapse;
  margin-bottom: 15px;
}
td, th{
  text-align: center;
  border: solid 1px #ccc;
}
th:last-child{
  width: 87px;
}
.rooms-section{
  display: flex;
  justify-content: space-between;
}
.item-room{
  position: relative;
  width: 100px;
  height: 150px;
  border: 1px solid green;
  margin: 10px
}
.item-room__title{
  position: absolute;
  bottom: -25px;
  left: 0;
}
.item-bulb{
  display: inline-block;
  width: 12px;
  height: 20px;
  margin: 5px;
  background: url("../assets/images/bulb.png") no-repeat 50% 50%;
  background-size: cover;
}
</style>
