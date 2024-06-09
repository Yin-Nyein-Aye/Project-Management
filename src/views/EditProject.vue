<template>
  <h1>Edit Project</h1>
  <form @submit.prevent="updateProject">       
    <label>Project Title</label>
    <input type="text" v-model="title">
    <label>Project Detail</label>
    <input type="text" v-model="detail">
    <button>Submit</button>
  </form>
</template>

<script>
export default {
    props: ['id'],
    data(){
      return{
        title:"",
        detail:"",
        api:"http://localhost:3000/projects/"
      }
    },
    mounted(){
      fetch(this.api+this.id)
      .then((res)=>{
        return res.json()
      })
      .then((datas)=>{
        this.title=datas.title;
        this.detail=datas.detail;
      })
      .catch((err)=>{
        console.log(err);
      })
    },
    methods:{
      updateProject(){
        fetch(this.api+this.id,{
          method : "PATCH",
          headers : {
            "Content-type" : "application/json"
          },
          body:JSON.stringify({
            title : this.title,
            detail : this.detail
          })
        })
        .then(()=>{
          this.$router.push('/')
        })
        .catch((err)=>{
          console.log(err)
        })
      }
    }
}
</script>
<style>

</style>