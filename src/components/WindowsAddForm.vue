<template>
    <form @submit="submitForm" method="post">

        <label for="windowname">Window name :</label>
        <input type="text" id="windowname" name="windowname" v-model="windowName"><br>

        <label for="roomId">Room ID :</label>
        <input type="text" id="roomId" name="roomId" v-model="roomId"><br>


        <label for="windowStatus">Window Status :</label>
        <input type="text" id="windowStatus" name="windowStatus" v-model="windowStatus"><br>

        <input type="submit" value="Envoyer le formulaire">
    </form>
</template>

<script>
export default {
    name: 'WindowsAddForm',
    data: function() {
        return {
            windowName: '',
            roomId: '',
            windowStatus: ''
        }
    },
    methods: {
        submitForm: function(e) {
            e.preventDefault();
            let window = { "id": null, "name": this.windowName, "roomId": this.roomId, "windowStatus": this.windowStatus };
            this.$emit('form-submitted', window); 
        }
    }
}
</script>