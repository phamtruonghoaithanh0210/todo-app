<template>
  <div class="container">
    <h2 class="text-center mt-5">hello World</h2>

    <!-- Input -->
    <div class="d-flex">
        <input v-model="task" type="text" placeholder="Enter Task" class="form-control">
        <button @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
    </div>


    <!-- Task Table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task,index) in tasks" :key="index">
          <td>{{task.name}}</td>
          <td>{{task.status}}</td>
          <td>
            <div class="text-center" @click="editTask(index)">
              <font-awesome-icon icon="fa-solid fa-pen" />
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(index)">
              <font-awesome-icon icon="fa-solid fa-trash" />
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      task : '',
      editedTask : null,
      tasks : [
        {
          name: "Ngủ Dậy Lúc 9h.",
          status: "to-do"
        },
        {
          name: "Ăn Sáng",
          status: "in-progress"
        },
      ]
    }
  },

  methods:{
    submitTask(){
      if(this.task.length === 0) return;

      if(this.editedTask === null){
        this.tasks.push({
          name: this.task,
          status: 'to-do'
        })
      }else{
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null
      }

      this.task = ''
    },

    deleteTask(index){
      this.tasks.splice(index,1)
    },

    editTask(index){
      this.task = this.tasks[index].name
      this.editedTask = index
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
