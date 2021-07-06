<template>
  <div class="container">
    <h2 class="text-center mt-5">Vue To-Do App</h2>

    <!-- INPUT -->
    <div class="d-flex">
      <input
        v-model="task"
        type="text"
        placeholder="Enter Task"
        class="form-control"
      />
      <button @click="submitTask" class="btn btn-warning rounded-0">
        Submit
      </button>
    </div>

    <!--      TABLE TASK    -->
    <table class="table table-bordered mt-4">
      <thead>
        <tr>
          <th scope="col">Task(s) List</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in allTasks" :key="index">
          <td>
            <span :class="{ 'task-completed': task.status === 'completed' }">
              {{ task.name }}
            </span>
          </td>
          <td style="width: 200px">
            <span
              v-on:click="changeStatus(index)"
              :class="{
                'hilight-warning': task.status === 'to-do',
                'hilight-remind': task.status === 'in-progress',
                'hilight-succeed' : task.status === 'completed',
              }"
              class="pointer">
              {{ firstCharUpper(task.status) }}
            </span>
          </td>
          <td>
            <div class="text-center" @click="editPressed(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center" v-on:click="deletePress(index)">
              <span class="fa fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "stickynote",
  props: {
    msg: String,
  },
  data() {
    return {
      task: "",
      toEditTask: null,
      allTasks: [
        {
          name: "Buy Battery",
          status: "to-do",
        },
        {
          name: "Revise CBCT chapter 2",
          status: "in-progress",
        },
        {
          name: "Revise CBCT chapter 12",
          status: "completed",
        },
      ],
      availStatuses: ["to-do", "in-progress", "completed"],
    };
  },
  methods: {
    submitTask() {
      // If not written any, return nothing
      if (this.task.length === 0) return;
      // If toEditTask not selected, meaning user want to create new task
      if (this.toEditTask === null) {
        this.allTasks.push({
          name: this.task,
          status: "to-do", // Satuts for new task will always be to-do
        });
      }
      //
      else {
        this.allTasks[this.toEditTask].name = this.task;
        this.toEditTask = null;
      }
      // Clear the placeholde after submit the task
      this.task = "";
    },
    editPressed(index) {
      this.task = this.allTasks[index].name;
      // assign the task into to-edit-task
      this.toEditTask = index;
    },
    changeStatus(index) {
      // The idea is to loop over all status in each click
      // 1. Figureout next value of task status
      // 2. Find the index of current status inside available status
      // 3. incremnt it, if bigger than 2, set it back to 0
      console.log(
        "Index before : " +
          this.availStatuses.indexOf(this.allTasks[index].status)
      );
      let newIndex = this.availStatuses.indexOf(this.allTasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.allTasks[index].status = this.availStatuses[newIndex];
      console.log(
        "Index after : " +
          this.availStatuses.indexOf(this.allTasks[index].status)
      );
    },
    deletePress(index) {
      this.allTasks.splice(index, 1);
    },
    firstCharUpper(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },
  },
};
</script>



<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.pointer {
  cursor: pointer;
}
.task-completed {
  text-decoration: line-through;
}
</style>
