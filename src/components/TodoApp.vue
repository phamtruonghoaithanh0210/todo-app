<template>
  <div class="container">
    <div class="row">
      <div class="col"></div>
      <div class="col-8">
          <h2 class="text-center mt-5">Todo Apps</h2>

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
              <td>
                <span :class="{'finished': task.status === 'finished'}">
                  {{task.name}}
                </span>
              </td>
              <td  style="width: 120px">
                <span @click="changeStatus(index)" class="pointer"
                  :class="{'text-danger': task.status === 'to-do',
                    'text-warning': task.status === 'in-progress',
                    'text-success': task.status === 'finished'}">
                  {{ firstCharUpper(task.status)}}
                </span>
              </td>
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
      <div class="col"></div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'ToDo App',
  props: {
    msg: String
  },
  data(){
    return{
      task : '',
      editedTask : null,
      avaiableStatuses: ['to-do', 'in-progress', 'finished'],
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
      this.$swal('Add task', 'Add task successful !', 'success');
    },

    deleteTask(index){
      this.tasks.splice(index,1)
      this.$swal('Delete task', 'Delete task successful !', 'success');
    },

    editTask(index){
      this.task = this.tasks[index].name
      this.editedTask = index
    },

    changeStatus(index){
      let newIndex = this.avaiableStatuses.indexOf(this.tasks[index].status);
      if(++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.avaiableStatuses[newIndex]

      this.$swal('Change status', `${this.avaiableStatuses[index]} to ${this.avaiableStatuses[newIndex]} successful`, 'success');
    },

    firstCharUpper(str){
      return str.charAt(0).toUpperCase() + str.slice(1);
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pointer {
  cursor: pointer;
}

.finished {
  text-decoration: line-through;
}
</style>
