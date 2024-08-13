<template>
  <div   class="container" style="max-width: 600px">
    <h2   class="text-center mt-5 ">TO-DO LIST</h2>

    <div  class="d-flex mt-5">
      <input
        type="text"
        v-model="task"
        placeholder="Enter task "
        class="styled-input"
      />
      <button class="btn btn-success rounded-0 my-custom-button" @click="submitTask">
        SUBMIT
      </button>
    </div>

    <table class="table table-bordered mt-5 ">
      <thead>
        <tr>
          <th scope="col" class="text-center">Task</th>
          <th scope="col" class="text-center">Status</th>
          <th scope="col" class="text-center">Edit</th>
          <th scope="col" class="text-center">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <span :class="{ 'line-through': task.status === 'finished' }">
              {{ task.name }}
            </span>
            <div class="creation-time">
      Created at: {{ formatDate(task.createdAt) }}
    </div>
          </td>
          <td>
            <span
              class="text-center custom"
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
            <div @click="deleteTask(index)">
              <span class="fa fa-trash pointer"></span>
            </div>
          </td>
          <td class="text-center">
            <div @click="editTask(index)">
              <p class="fa fa-pen pointer"></p>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      task: "",
      editedTask: null,
      statuses: ["to-do", "in-progress", "finished"],

      tasks: [
        {
          name: "Sleep on time",
          status: "to-do",
        },
        {
          name: "Car fixing.",
          status: "in-progress",
        },
        {
          name: "Breakfast",
          status: "finished",
        },
      ],
    };
  },

  methods: {

  
    capitalizeFirstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },

  formatDate(date) {
    if (!date) return '';
    return new Date(date).toLocaleString();
  },

    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },

 
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

   
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

   
    submitTask() {
      if (this.task.length === 0) return;
      const newTask = {
    name: this.task,
    status: "to-do",
    createdAt: new Date() 
  };

  if (this.editedTask !== null) {
    
    newTask.createdAt = this.tasks[this.editedTask].createdAt;
    this.tasks[this.editedTask] = newTask;
    this.editedTask = null;

      } else {
    this.tasks.push(newTask);
  }

  this.task = "";
},
  },
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
.my-custom-button {
  background-color: blueviolet !important; 
  color: white !important; 
}
.text-center custom {
  display: block;
  text-align: center;
  cursor: pointer; 
  padding: 5px; 
}

.text-danger {
  color: #dc3545; 
}

.text-success {
  color: #28a745;
}

.text-warning {
  color: #ffc107; 
}
.noselect {
  -webkit-touch-callout: none; 
  -webkit-user-select: none; 
    -khtml-user-select: none; 
  -moz-user-select: none; 
  -ms-user-select: none; 
  user-select: none; 
}
.text-center {
  text-align: center;
  margin-top: 2rem; 
  color: #3498db; 
  font-family: 'Arial', sans-serif; 
  font-size: 2 rem; 
  text-shadow: 2px 2px 4px rgba(0,0,0,0.1); 
  transition: transform 0.3s ease; 
}
.styled-input {
  width: 100%;
  padding: 10px;
  margin: 10px 0;
  border-radius: 5px;
  border: 1px solid #ccc;
  box-sizing: border-box;
}
.text-center:hover {
  transform: scale(1.05); 
  color: #2ecc71; 
}
.line-through {
  text-decoration: line-through;
}


</style>

