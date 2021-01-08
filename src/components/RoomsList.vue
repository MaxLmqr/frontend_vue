<template>
  <div class="rooms-list pt-3">
    <rooms-list-item 
      v-for="room in rooms"
      :room="room"
      :key="room.id"  
      @Room-updated="updateRoom"
    >
    </rooms-list-item>
  </div>
</template>


<script>
import axios from 'axios';
import {API_HOST} from '../config';
import RoomsListItem from './RoomsListItem';

export default {
  components: {
    RoomsListItem
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
    updateRoom(newRoom) {
      /* Find the place of room objectw ith the same Id in the array, and replace it */
      let index = this.rooms.findIndex(room => room.id === newRoom.id);
      this.rooms.splice(index, 1, newRoom);
    }
  }
}
</script>
