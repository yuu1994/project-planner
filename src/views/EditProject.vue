<template>
  <form @submit.prevent="updateProject">
    <div>
      <label>Project Title</label>
      <input type="text" v-model="title" />
    </div>
    <div class="">
      <label>Project Detail</label>
      <input type="text" v-model="detail" />
    </div>
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      detail: "",
      api: "http://localhost:3000/projects/",
    };
  },
  mounted() {
    fetch(this.api + this.id)
      .then((res) => {
        return res.json();
      })
      .then((data) => {
        this.title = data.title
        this.detail = data.detail
      })
      .catch((err) => {
        console.log(err);
      });
  },
  methods : {
    updateProject(){
      let updateRoute = this.api + this.id 
      fetch(updateRoute,{
        method : "PATCH",
        headers : {"Content-Type" : "application/json"},
        body :JSON.stringify({
          title : this.title,
          detail : this.detail
        })
      })
      .then(()=>{
        this.$router.push({name:'home'})
      })
      .catch((err)=>{
        console.log(err)
      })
    }
  }
};
</script>
<style></style>
