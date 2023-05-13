<template>
  <div class="home">
    <h2>Projects</h2>
    <FilterProject @currentValue="current = $event" :current="current" ></FilterProject>
    <div class="" v-for="project in filterProjects" :key="project.id">
      <SingleProject :project="project" @deleteProject="deleteProject" @completeProject="completeProject" ></SingleProject>
    </div>
  </div>
</template>

<script>

import FilterProject from '../components/FilterProject'
import SingleProject from '../components/SingleProject'
export default {
  data(){
    return {
      projects : [],
      current : ""
    }
  },
  name: 'HomeView',
  components: {
    FilterProject,
    SingleProject,

  },
  methods : {
    deleteProject(deleteId){
      this.projects = this.projects.filter((project)=>{
        return project.id != deleteId
      })
    },
    completeProject(completeId){
      let completeProject = this.projects.find((project)=>{
        return project.id == completeId
      })
      completeProject.complete = !completeProject.complete
    },
    // currentValue(value){
    //   return this.current = value
    // }
  },
  computed : {
    filterProjects(){
      return this.projects.filter((project)=>{
        if(this.current == 'complete'){
          return project.complete == true
        }
        if(this.current == 'ongoing'){
          return project.complete == false
        }
        return project
      })
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then((response)=>{
      return response.json()
    })
    .then((data)=>{
      this.projects = data
    })
    .catch((error)=> {
      console.log(error)
    })
  }
}
</script>
