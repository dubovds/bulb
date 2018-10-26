<template>
  <div id="add-room">
    <div class="">
      <input v-model="newRoom">
      <button @click="addRoom">Add Room</button>
    </div>

    <div class="room-block"  v-for="(room) in rooms"
      v-bind:key="room.room">
        <span class="room-block__title">{{ room.room }}</span>
        <button class="room-block__burron-del" v-on:click="removeRoom()">Удалить</button>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      newRoom: '',
      rooms: [],
      roomBlock: 'room-block'
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
  },
  methods:{
    addRoom: function () {
      this.rooms.push({
        room:this.newRoom,
        roomBlock: this.roomBlock
      });
      this.newRoom = '';
      this.saveRooms();
    },
    removeRoom(x) {
      this.rooms.splice(x, 1);
      this.saveRooms();
    },
    saveRooms() {
      const parsed = JSON.stringify(this.rooms);
      localStorage.setItem('rooms', parsed);
    }
  }
}
</script>

<style lang="css">
.room-block{
  position: relative;
  display: inline-block;
  width: 100px;
  height: 200px;
  border: 2px solid grey;
  margin: 10px 5px
}
.room-block__title{
  position: absolute;
  bottom: -25px
}
.room-block__burron-del{
  position: absolute;
  bottom: -25px;
  right: -30px
}
</style>
