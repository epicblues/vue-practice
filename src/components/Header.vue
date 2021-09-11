<template>
    <header>
        <h1>{{title}}</h1>
        
        <Button v-show="homePage"
        :text="showAddTask ? 'hide' : 'Add Task'" 
        :color="showAddTask ? 'red' : 'green'" 
        @click="$emit('show-form')"/>
        
    </header>
    
</template>

<script>
import Button from './Button'



export default {
    name:'Header',
    props: {
        title: {
            type:String,
            default:'Hello World Default',
        },
        showAddTask:Boolean
    },
    data() {
        return {
            form : false,

        }
    }
    ,
    components: {
        Button,

    },
    methods: {
    },
    computed: {
        homePage() {
            if(this.$route.path ==='/') {
                return true;
            } else {
                return false;
            }
        }
    }
    

}
</script>

<style scoped>
     header {
        display:flex;
        justify-content: space-between;
        align-items:center;
        margin-bottom:20px;
    }
</style>
   
