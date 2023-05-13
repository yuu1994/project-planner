<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="flexing">
      <div class="" @click="showDetail = !showDetail">
        <h3>{{ project.title }}</h3>
      </div>
      <div class="">
        <span class="material-symbols-outlined" @click="deleteProject">
          delete
        </span>
        <router-link :to="{ name:'editproject',params:{id:project.id}}">
          <span class="material-symbols-outlined"> edit </span>
        </router-link>
        <span
          class="material-symbols-outlined"
          @click="completeProject"
          :class="{
            greenicon: project.complete,
            redicon: project.complete == false,
          }"
        >
          done
        </span>
      </div>
    </div>
    <p v-if="showDetail">{{ project.detail }}</p>
  </div>
</template>
<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetail: false,
      api: "http://localhost:3000/projects/",
    };
  },
  methods: {
    deleteProject() {
      let deleteRoute = this.api + this.project.id;
      fetch(deleteRoute, { method: "DELETE" })
        .then(() => {
          this.$emit("deleteProject", this.project.id);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    completeProject() {
      let completeRoute = this.api + this.project.id;
      fetch(completeRoute, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          complete: !this.project.complete,
        }),
      }).then(() => {
        this.$emit("completeProject", this.project.id);
      });
    },
  },
};
</script>

<style>
.project {
  background-color: rgba(205, 213, 215, 0.551);
  margin: 6px;
  padding: 6px;
  border-left: 5px solid crimson;
  border-radius: 10px;
}
h3 {
  color: indigo;
  cursor: pointer;
}
.flexing {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
span {
  margin-left: 10px;
  color: black;
}
span:hover {
  color: rgb(139, 130, 130);
  cursor: pointer;
}
.complete {
  border-left: 5px solid green;
}
.greenicon {
  color: green;
}
.redicon {
  color: crimson;
}
</style>
