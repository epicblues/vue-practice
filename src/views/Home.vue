<template>
    
    <AddTask @save-task="saveTask" v-show="showAddTask"/>
    
    <Tasks 
      @delete-task="deleteTask" 
      @change-reminder="changeReminder"
      :tasks = "tasks"/>
</template>

<script>
    import Tasks from '../components/Tasks.vue';
    import AddTask from '../components/AddTask.vue';
    export default {
        name:"Home",
        components: {
            Tasks,
            AddTask
        },
        data() {
            return {
                tasks : [],
                
            }
        },
        props : {
            showAddTask:Boolean
        },
        async created() {
        this.tasks =await this.fetchTasks();
            },
        methods: {
    async deleteTask(id) {
      if(!confirm('Are you sure?')) return;
      
      const res = await fetch('api/tasks/' + id , {
        method:"DELETE"
      })
      
      res.status === 200 ? (this.tasks = this.tasks.filter(task => task.id !== id)) : alert('Request Didn\'t Work');
      


    },
    async changeReminder(id) {
      let fixedTask = await this.fetchTask(id);
      
      const res = await fetch('api/tasks/' + id, {
        method:"PATCH",
        headers:{
          "Content-Type" : "application/json"
        },
        body : JSON.stringify({...fixedTask, reminder:!fixedTask.reminder})
      })
      fixedTask = await res.json();
      const fixedTasks = this.tasks.map(task => 
        task.id === id ? fixedTask : task
      )
      this.tasks = fixedTasks;

    },
    async saveTask(task) {
      const res = await fetch('api/tasks', {
        method:'POST',
        headers: {
          "Content-Type" : "application/json; charset=utf-8" 
        },
        body: JSON.stringify(task)
      })
      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },
    
    async fetchTasks(){
      const res = await fetch('api/tasks')
      const data = await res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch('api/tasks/' + id);
      const data = await res.json();
      return data;
    }
    
  },
  

    }
</script>