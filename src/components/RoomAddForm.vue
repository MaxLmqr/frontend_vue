<template>
    <form @submit="submitForm" method="post">

        <label for="roomname">Room name :</label>
        <input type="text" id="roomname" name="roomname" v-model="roomName"><br>

        <label for="currentTemperature">Current temperature</label>
        <input type="text" id="currentTemperature" name="currentTemperature" v-model="currentTemperature"><br>


        <label for="targetTemperature">Target Temperature :</label>
        <input type="text" id="targetTemperature" name="targetTemperature" v-model="targetTemperature"><br>

        <input type="submit" value="Envoyer le formulaire">
    </form>
</template>

<script>
export default {
    name: 'WindowsAddForm',
    data: function() {
        return {
            roomName: '',
            currentTemperature: '',
            targetTemperature: ''
        }
    },
    methods: {
        submitForm: function(e) {
            e.preventDefault();
            let room = {
            "buildingId": -10,
            "current_temperature": this.currentTemperature,
            "floor": 0,
            "id": null,
            "name": this.roomName,
            "target_temperature": this.targetTemperature
            };
            this.$emit('form-submitted', room); 
        }
    }
}
</script>