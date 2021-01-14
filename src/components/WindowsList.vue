<template>
  <div class="windows-list pt-3">
    <windows-list-item 
      v-for="window in windows"
      :window="window"
      :key="window.id"  
      @window-updated="updateWindow"
    >
    </windows-list-item>
    <windows-add-form v-bind:rooms="rooms" @form-submitted="submitForm"></windows-add-form>
  </div>
</template>


<script>
import axios from 'axios';
import Vue from 'vue';
import {API_HOST} from '../config';
import WindowsListItem from './WindowsListItem';
import WindowsAddForm from './WindowsAddForm';

export default {
  components: {
    WindowsListItem,
    WindowsAddForm
  },
  name: 'WindowsList',
  data: function() {
    return {
      /* Initialize windows with an empty array, while waiting for actual data to be retrieved from the API */
      windows: [],
      rooms: []
    }
  },
  created: async function() {
    let response = await axios.get(`${API_HOST}/api/windows`).catch(() => {
      Vue.toasted.show("Could not load windows", {duration:5000,position:'bottom-center'});
    });
    let windows = response.data;
    this.windows = windows;

    let response2 = await axios.get(`${API_HOST}/api/rooms`).catch(() => {
      Vue.toasted.show("Could not load rooms", {duration:5000,position:'bottom-center'});

    });
    let rooms = response2.data;
    this.rooms = rooms;
  },
  methods: {
    updateWindow(newWindow) {
      /* Find the place of window objectw ith the same Id in the array, and replace it */
      let index = this.windows.findIndex(window => window.id === newWindow.id);
      if (newWindow === '') {
        this.windows.splice(index, 1);
      } else {
        this.windows.splice(index, 1, newWindow);
      }
    },
    async submitForm(window) {
      let response = await axios.post(`${API_HOST}/api/windows`,window);
      let newWindow = response.data;
      this.windows.push(newWindow);
    }
  }
}
</script>
