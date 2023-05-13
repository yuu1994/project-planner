<template>
  <form @submit.prevent="createProject">
    <div class="">
      <label>Project Title</label>
      <input type="text" v-model="title" />
    </div>
    <div class="">
      <label>Project Detail</label>
      <input type="text" v-model="detail" />
    </div>
    <button>Create</button>
  </form>
</template>

<script>
export default {
  data(){
    return {
      title : "",
      detail : ""
    }
  },
  methods: {
    createProject(){
      fetch('http://localhost:3000/projects',{
        method:"POST",
        headers : {"Content-Type" : "application/json"},
        body :JSON.stringify({
            title : this.title ,
            detail : this.detail,
            complete : false
        })
      })
      .then(()=>{
        this.$router.push({name:"home"})
      })
      .catch((error)=> {
        console.log(error)
      })
    }
  }
};
</script>

<style>
form{
  width: 500px;
  padding: 0 50px;
  color: gray;
}
label {
  display: block;
  margin: 6px auto;
}
input {
  width: 100%;
  border: 0;
  border-bottom: 1px solid gray;
  margin: 6px auto;
  height: 30px;
}
button {
  display: block;
  margin: 10px auto;
  padding: 8px 16px;
  background-color: rgba(0, 128, 0, 0.808);
  color: white;
  border: none;
  border-radius: 10px;
}
button:hover {
  background-color: green;
}
</style>
