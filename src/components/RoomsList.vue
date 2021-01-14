<template>
  <div class="rooms-list pt-3">
    <rooms-list-item 
      v-for="room in rooms"
      :room="room"
      :key="room.id" 
      @room-deleted="deleteRoom"
    >
    </rooms-list-item>
    <room-add-form v-bind:buildings="buildings" @form-submitted="submitForm"></room-add-form>
  </div>
</template>


<script>
import axios from 'axios';
import Vue from 'vue';
import {API_HOST} from '../config';
import RoomsListItem from './RoomsListItem';
import RoomAddForm from './RoomAddForm';

export default {
  components: {
    RoomsListItem,
    RoomAddForm
  },
  name: 'RoomsList',
  data: function() {
    return {
      /* Initialize rooms with an empty array, while waiting for actual data to be retrieved from the API */
      rooms: [],
      buildings: []
    }
  },
  created: async function() {
    let response = await axios.get(`${API_HOST}/api/rooms`).catch(() => {
      Vue.toasted.show("Could not load rooms", {duration:5000,position:'bottom-center'});
    });
    let rooms = response.data;
    this.rooms = rooms;

    let response2 = await axios.get(`${API_HOST}/api/buildings`).catch(() => {
      Vue.toasted.show("Could not load buildings", {duration:5000,position:'bottom-center'});
    });
    let buildings = response2.data;
    this.buildings = buildings;
  },
  methods: {
    deleteRoom(id) {
      /* Find the place of room objectw ith the same Id in the array, and replace it */
      let index = this.rooms.findIndex(room => room.id === id);
      this.rooms.splice(index, 1);
    },
    async submitForm(room) {
      let response = await axios.post(`${API_HOST}/api/rooms`,room);
      let newRoom = response.data;
      this.rooms.push(newRoom);
    }
  }
}
</script>
