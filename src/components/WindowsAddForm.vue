<template>
    <div class="card mt-5 mb-5">
        <div class="card-header">
            Add a new Window
        </div>
        <div class="card-body">
            <form @submit="submitForm" method="post">
                <div class="form-row">
                    <input placeholder="Window Name" class="form-control" type="text" id="windowname" name="windowname" v-model="windowName"><br>
                    <select class="form-control" name="names" id="roomName" v-model="roomId">
                        <option value="" disabled>Select a Room...</option>
                        <option v-for="room in rooms" :room="room" :key="room.id" :value="room.id">{{room.name}}</option>
                    </select><br>
                    <select class="form-control" name="names" id="windowStatus" v-model="windowStatus">
                        <option value="" disabled>Select a window status...</option>
                        <option value ="OPEN" selected="selected">OPEN</option>
                        <option value="CLOSED">CLOSED</option>
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
    props: ["rooms"],
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