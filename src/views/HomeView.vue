<template>
  <h1>Home</h1>
    <FilterNav @filterValue="current=$event" :current="current"></FilterNav>
    <div v-for="project in filterProjects" :key="project.id">    
      <DetailsData :project="project" @delete="deleteProject" @complete="completeProject" />
    </div>    
</template>

<script>
import DetailsData from '../components/DetailsData'
import FilterNav from '../components/FilterNav'

export default {
  name: 'HomeView',
  components:{
    DetailsData,
    FilterNav
  },
  data(){
    return{
      projects:[],
      current:"all"
    }
  },
  computed:{
    filterProjects(){
      if(this.current === 'complete'){
        return this.projects.filter((p)=>{
          return p.complete;
        })
      }
      if(this.current === 'ongoing'){
        return this.projects.filter((p)=>{
          return !p.complete;
        })
      }
      return this.projects;
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then((response)=>{
      return response.json()
    })
    .then((datas)=>{
      this.projects=datas
    }) 
    .catch(()=>{

    })
  },
  methods:{
    deleteProject(id){
      this.projects = this.projects.filter(project=>{
        return project.id != id;
      })
    },
    completeProject(id){
      let completePjId = this.projects.find(project=>{
        return project.id === id;
      });
      completePjId.complete = !completePjId.complete;
    }
  }
}
</script>
