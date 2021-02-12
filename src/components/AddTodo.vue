<template>
    <div class="add-todos">
        <form @submit="addTodo" class="form">
            <input type="text" placeholder="add todo" v-model="title"/>
            <input type="submit"/>
        </form>
        
    </div>
</template>

<script>
import uuid from 'uuid'
export default {
    name:'AddTodo',
    data(){
        return {
            title:''
        }
    },

    methods:{
        addTodo(e){
            e.preventDefault()
        
        if(this.title){
            const newTodo = {
            id:uuid.v4(),
            title:this.title,
            completed:false
        }
            this.$emit('add-todo',newTodo)
            this.title = ''
        }
        }
        
    }


}
</script>

<style scoped>

.add-todos{
    margin-top: 4rem;
    margin-bottom: 2rem;
    /* display: flex;
    justify-content: center;
    width:100%; */
}
.form{

     display: flex;
    justify-content: center;
   
}
input[type="text"]{
    width:15rem;
   padding:0.5rem 0.5rem;
    border-radius:3px;
    border-width: thin;
    margin-right: 8px;
    outline-color:#748277;
}

input[type="text"]:focus-within{

   /* border-color:red; */
   outline-color: #84fa9e;
}
input[type="submit"]{
    background-color: #ad103c;
    outline: none;
    border-radius:3px;
    color:white
}

input[type="submit"]{
    outline-color: none;
    padding:0.8rem 2rem
}


</style>