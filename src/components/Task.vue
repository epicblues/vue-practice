<template>
    <div :class="['task', task.reminder?'reminder':'']" 
    @dblclick="$emit('change-reminder', task.id)">
        <h3>{{task.text}}
            <i class="fas fa-times" @click="$emit('delete-task',task.id)"></i>
        </h3>
        <p>{{task.day}}</p>
    </div>
  
</template>

<script>
import Button from './Button.vue';


export default {

    props : {
        task : Object
    },
    components : {
        Button,
    },
    methods : {
    },
    
    
}
</script>

<style scoped>
.fas {
    color:red;
}

.task {
    background:#e6e6e6;
    margin:5px;
    padding: 10px 20px;
    cursor:pointer;
}

.task.reminder {
    border-left: 5px solid green;
}

.task >h3 {
    display:flex;
    align-items: center;
    justify-content: space-between;
    
}


</style>