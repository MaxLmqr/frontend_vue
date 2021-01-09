<template>
  <div class="windows-list pt-3">
    <windows-list-item 
      v-for="window in windows"
      :window="window"
      :key="window.id"  
      @window-updated="updateWindow"
    >
    </windows-list-item>
    <windows-add-form @form-submitted="submitForm"></windows-add-form>
  </div>
</template>


<script>
import axios from 'axios';
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
      windows: []
    }
  },
  created: async function() {
    let response = await axios.get(`${API_HOST}/api/windows`);
    let windows = response.data;
    this.windows = windows;
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
