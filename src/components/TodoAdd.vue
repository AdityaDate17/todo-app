<template>
  <div class="container" style="max-width: 600px">
    <!-- Heading -->
    <h2 class="text-center mt-5">Todo Task</h2>

    <!-- Input -->
    <div class="d-flex mt-5">
      <input
        type="text"
        v-model="task"
        placeholder="Enter task"
        class="w-100 form-control"
      />
      <button class="btn btn-primary rounded-0" @click="submitTask">
        Submit
      </button>
    </div>

    <!-- Task table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col" style="width: 110px">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <span :class="{ 'line-through': task.status === 'finished' }">
              {{ task.name }}
            </span>
          </td>
          <td>
            <span
              class="pointer noselect"
              @click="changeStatus(index)"
              :class="{
                'text-danger': task.status === 'to-do',
                'text-success': task.status === 'finished',
                'text-warning': task.status === 'in-progress',
              }"
            >
              {{ capitalizeFirstChar(task.status) }}
            </span>
          </td>
          <td class="text-center">
                <button type="button" @click="deleteTask(index)" class="btn btn-success rounded-0">Delete</button>
          </td>
          <td class="text-center">
            <div v-if="!isDisabled">
                <button type="button" @click="editTask(index)" class="btn btn-warning rounded-0">Edit</button>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {

  data() {
    return {
      task:"",
      editedTask: null,
      statuses: ["to-do", "in-progress", "finished"],
      isDisabled:false,

      /* Status could be: 'to-do' / 'in-progress' / 'finished' */
      tasks: [
        {
          name:"Learn Golang1.6@",
          status: "to-do",
        },
      ],
    };
  },

  methods: {
    /**
     * Capitalize first character
     */
    capitalizeFirstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },

    /**
     * Change status of task by index
     */
    changeStatus(index) {
      console.log("change status index value",index)     
    //   let newIndex = this.statuses.indexOf(this.tasks[index].status);
      let i = this.statuses.indexOf(this.tasks[index].status);
      console.log("new index",i)  
      if(++i>2) 
            
            i=0 ;
            this.tasks[index].status = this.statuses[i];
            console.log("updated status",this.tasks[index].status ) 
            console.log("new index inside loop",i)
           

    },

    /**
     * Deletes task by index
     */
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    /**
     * Edit task
     */
    editTask(index) {
        console.log(this.index)
      this.task = this.tasks[index].name;
      this.editedTask = index;
      if(this.tasks[index].status=='finished'){
        this.isDisabled = true;
        
      }
      console.log(this.isDisabled)
      console.log( this.tasks[index].name)
       this.task = "";
    },

    /**
     * Add / Update task
     */
    submitTask() {
      if (this.task.length === 0) return;

      /* We need to update the task */
      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      } else {
        /* We need to add new task */
        this.tasks.push({
          name: this.task,
          status: "todo",
        });
      }

      this.task = "";
    },
  },

//   computed:{
//     statusName(){
//         return [
//            "to-do",
//            "in-progress",
//            "finished"
//         ]
//     }
//   }
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
.noselect {
  -webkit-touch-callout: none; /* iOS Safari */
  -webkit-user-select: none; /* Safari */
  -khtml-user-select: none; /* Konqueror HTML */
  -moz-user-select: none; /* Old versions of Firefox */
  -ms-user-select: none; /* Internet Explorer/Edge */
  user-select: none; /* Non-prefixed version, currently
                                  supported by Chrome, Edge, Opera and Firefox */
}
.line-through {
  text-decoration: line-through;
}
</style>