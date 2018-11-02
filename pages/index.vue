<template>
  <section class="container" id="app">
    <div class="top">
      <h1 class="title">
        Accounting light bulbs in the house
      </h1>
      <div class="room__section">
        <div class="add-room__input-section">
          <input type="text" class="form-control" v-model='newRoom' placeholder="Enter your room">
          <button type="button" class="btn btn-success" name="button" @click='addRoom'>+</button>
        </div>
        <div class="add-room__list-section">
          <div class="item-room"
               v-for="(room, x) in rooms"
               v-bind:key="room.id">

               <div class="" v-for="bulb in bulbs" v-bind:key="bulb.id"
                             v-if="bulb.roomId == room.id"
                             v-bind:class="itemBulb">
               </div>

            <span class="item-room__title">{{ room.label }}</span>
            <button class="btn btn-danger item-room__button" v-on:click="removeRoom(x)">-</button>
          </div>
        </div>
      </div>

      <div class="rooms-section">

      </div>
    </div>
      <div id="bulb-section">
        <!-- <form class="form-bulb"> -->
        <form class="form-bulb"
              v-on:submit.prevent="addBulb"
              v-show="hasRooms">
          <div class="form-item">
            <label for="new-room">Select room</label>
            <select class="form-control" v-model='selected'>
              <option disabled value="Выберите комнату">Select room</option>
              <option v-for='room in rooms'
                      v-bind:value= 'room.id'
                      v-bind:key= 'room.key'>
                          {{ room.label }}
              </option>
            </select>
          </div>
          <div class="form-item">
            <label for="new-position">Position of bulb</label>
            <input class="form-control"
              v-model="newPosition"
              id="new-position"
              placeholder="Left corner"
            >
          </div>
          <div class="form-item">
            <label for="new-date">Installation date</label>
            <input class="form-control"
              v-model="newDate"
              id="new-date"
              placeholder="12.10.2018"
            >
          </div>
          <div class="form-item">
            <label for="new-garanty">Warranty up to</label>
            <input class="form-control"
              v-model="newGaranty"
              id="new-garanty"
              placeholder="10.2019"
            >
          </div>
          <button class="btn btn-success">Add the bulb</button>
        </form>

        <div class="content-section">

          <table v-show="hasRooms">
            <tr>
              <th>Room</th>
              <th>Position of balb</th>
              <th>Installation date</th>
              <th>Warranty up to</th>
              <th></th>
            </tr>
            <tr v-for="bulb in bulbs"
                v-bind:key="bulb.id"
                v-bind:title="bulb.titleRoom"
                v-bind:class="bulb.titleRoom">
              <td>
                  {{bulb.titleRoom}}
              </td>
              <td>
                  {{ bulb.titlePosition }}
              </td>
              <td>
                  {{ bulb.titleDate }}
              </td>
              <td>
                  {{ bulb.titleGaranty }}
              </td>
              <td>
                <button class="btn btn-danger" v-on:click="removeBulb()">-</button>
              </td>
            </tr>
          </table>
        </div>
      </div>
  </section>
</template>

<script>
import Vue from 'vue'
import AppLogo from '~/components/AppLogo.vue'

export default {
  components: {
    AppLogo
  },
  data () {
    return {
      rooms: [],
      bulbs: [],
      selected: '',
      newRoom: '',
      newDate: '',
      roomId: '',
      newPosition: '',
      newGaranty: '',
      nextIdRoom: 1,
      nextIdBulb: 1,
      itemBulb: 'item-bulb'
    }
  },
  mounted() {
    if (localStorage.getItem('rooms')) {
      try {
        this.rooms = JSON.parse(localStorage.getItem('rooms'));
      } catch(e) {
        localStorage.removeItem('rooms');
      }
    };
    if (localStorage.getItem('bulbs')) {
      try {
        this.bulbs = JSON.parse(localStorage.getItem('bulbs'));
      } catch(e) {
        localStorage.removeItem('bulbs');
      }
    }
  },
  computed: {
    hasRooms(){
      return this.rooms.length > 0;
    }
  },
  methods: {
    addRoom(){
      this.rooms.push({
        id: this.nextIdRoom++,
        label: this.newRoom
      });
      this.newRoom = '';
      this.saveRooms();
    },
    addBulb(){

      const selectedRoom = this.rooms.find((room) => {
        return room.id === this.selected;
      });

      this.bulbs.push({
        roomId: selectedRoom.id,
        itemBulb: this.itemBulb,
        id: this.nextIdBulb++,
        titleRoom: selectedRoom.label,
        titlePosition: this.newPosition,
        titleDate: this.newDate,
        titleGaranty: this.newGaranty
      }),
      this.newPosition = '',
      this.newDate = '',
      this.newGaranty = '',
      this.selected = '',
      this.saveBulbs();
    },
    removeRoom(x) {
      this.rooms.splice(x, 1);
      this.saveRooms();
    },
    removeBulb(x) {
      this.bulbs.splice(x, 1);
      this.saveBulbs();
    },
    saveRooms() {
      const parsed = JSON.stringify(this.rooms);
      localStorage.setItem('rooms', parsed);
    },
    saveBulbs() {
      const parsed = JSON.stringify(this.bulbs);
      localStorage.setItem('bulbs', parsed);
    }

  }
}

</script>

<style>
.container {
  width: 1140px;
  margin: auto;
}
.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 50px;
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

.item-bulb{
  display: inline-block;
  width: 12px;
  height: 20px;
  margin: 5px;
  background: url("../assets/images/bulb.png") no-repeat 50% 50%;
  background-size: cover;
}
</style>
