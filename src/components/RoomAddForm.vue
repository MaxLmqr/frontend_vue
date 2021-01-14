<template>
<div class="card mt-5">
    <div class="card-header">
        Add a new Room
    </div>
    <div class="card-body">
        <form @submit="submitForm" method="post">
            <div class="form-row">
                <input placeholder="Room Name" class="form-control" type="text" id="roomname" name="roomname" v-model="roomName"><br>

                <input placeholder="Current Temperature" class="form-control" type="text" id="currentTemperature" name="currentTemperature" v-model="currentTemperature"><br>


                <input placeholder="Target Temperature" class="form-control" type="text" id="targetTemperature" name="targetTemperature" v-model="targetTemperature"><br>
                <select class="form-control" name="names" id="buildingName" v-model="buildingId">
                    <option value="" disabled>Select a Building...</option>
                    <option v-for="building in buildings" :building="building" :key="building.id" :value="building.id">{{building.name}}</option>
                </select><br>

                <input type="submit" value="Add">
            </div>
        </form>
    </div>
</div>
</template>

<script>
export default {
    name: 'WindowsAddForm',
    props: ["buildings"],
    data: function() {
        return {
            roomName: '',
            currentTemperature: '',
            targetTemperature: '',
            buildingId: ''
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