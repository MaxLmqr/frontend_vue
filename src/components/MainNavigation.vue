<template>
  <ul class="nav nav-tabs">
    <li class="nav-item">
      <a class="nav-link" @click="triggerWindowsMenu"  v-bind:class="{active: display==='windows'}" href="#">Windows</a>
    </li>
    <li class="nav-item">
      <a class="nav-link" @click="triggerRoomsMenu" v-bind:class="{active: display==='rooms'}" href="#" tabindex="-1">Rooms</a>
    </li>
  </ul>
</template>


<script>
export default {
  props: ['display'],
  name: 'MainNavigation',
  methods: {
    triggerWindowsMenu() {
      this.$emit("update-display","windows"); 
    },
    triggerRoomsMenu() {
      this.$emit("update-display","rooms"); 
    }
  } 
}
</script>