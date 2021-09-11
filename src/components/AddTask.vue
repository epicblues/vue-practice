<template>
    <form class="add-form"  @submit="saveTask" >
        <div class="form-control">
            <label>Task</label>
            <input type="text" placeholder="Add Task" id="task" name="text"
            v-model="text">
        </div>
        <div class="form-control">
            <label>Date</label>
            <input type="text" placeholder="Add Date & Time" id="day" v-model="day" name="day">
        </div>
        <div class="form-control-check">
            <label for="reminder">Set Reminder</label>
            <input type="checkbox" name="reminder" v-model="reminder"/>
        </div>
        <input type="submit" value="Save Task" class="btn btn-block">
    </form>
    
    
</template>

<script>


export default {
    name: 'AddTask',
    props: {

    },
    methods: {
        saveTask(event) {
            event.preventDefault();
            if(!this.text) {
                alert('Add Task!!')
                return;
            } else if(!this.day) {
                alert('Add Date!!');
                return;
            }
            const newTask = {
                id: Math.floor(Math.random()*1000000),
                text:this.text,
                day:this.day,
                reminder:this.reminder
            }
            this.$emit('save-task', newTask);
            this.text = '';
            this.day = '';
            this.reminder = false;
        }
    },
    data(){
        return {
            text:'',
            day:'',
            reminder:false
        }
    }
}
</script>

<style scoped>
    .add-form {
        margin-bottom: 40px;
    }

    

    .form-control {
        margin: 20px 0;
    }

    .form-control label {
        display:block;
    }

    .form-control input {
        width:100%;
        height:40px;
        margin:5px;
        padding : 3px 7px;
        font-size:17px
    }

    .form-control-check {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
</style>