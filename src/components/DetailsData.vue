<template>
<div class="project" :class="{complete:project.complete}">    
    <div class="flexing">
        <div>
            <h1 @click="showDetail=!showDetail">{{project.title}}</h1>            
            <p v-if="showDetail">{{project.detail}}</p>
        </div>
        <div>
            <span class="material-symbols-outlined" @click="deleteProject">
                delete
            </span>
            <router-link :to="{name:'editProject',params:{id:project.id}}">
                <span class="material-symbols-outlined">
                    edit
                </span>
            </router-link>            
            <span class="material-symbols-outlined" @click="selected">
                check
            </span>  
        </div>
    </div>  
</div>    
</template>

<script>
export default {
    props:['project'],
    data(){
        return{
            showDetail:false,
            api:"http://localhost:3000/projects/"
        }
    },
    methods:{
        deleteProject(){
            let deleteRoute = this.api+this.project.id;
            fetch(deleteRoute,{method:"DELETE"})
            .then(()=>{
                this.$emit("delete",this.project.id);
            })
            .catch((err)=>{
                console.log(err);
            })
        },
        selected(){
           let updateCompleteRoute=this.api+this.project.id;
           fetch(updateCompleteRoute,{
                method:"PATCH",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify(
                    {
                        complete:!this.project.complete
                    }
                )
           })
           .then(()=>{
                this.$emit("complete",this.project.id);
           })
           .catch((err)=>{
            console.log(err);
           })
        }
    }
}
</script>

<style>
.project{
    background: #fbf7f7;
    padding: 20px;
    margin: 10px;
    border-left: 8px solid crimson;
    border-radius: 5px 20px;
}
.project:hover{
    background: rgb(252, 252, 219);
}
h1{
    color: indigo;
}
.flexing{
    display: flex;
    justify-content: space-between;
    align-items: center;    
}
span{
    margin: 10px;
    cursor: pointer;
}
span:hover{
    color: #777;
}
h1{
    cursor: pointer;
}
.complete{
    border-left-color: green;
}
</style>