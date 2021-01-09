<template>
  <div class="rooms-list pt-3">
    <rooms-list-item 
      v-for="room in rooms"
      :room="room"
      :key="room.id"  
      @room-deleted="deleteRoom"
    >
    </rooms-list-item>
    <room-add-form @form-submitted="submitForm"></room-add-form>
  </div>
</template>


<script>
import axios from 'axios';
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
      rooms: []
    }
  },
  created: async function() {
    let response = await axios.get(`${API_HOST}/api/rooms`);
    let rooms = response.data;
    this.rooms = rooms;
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
