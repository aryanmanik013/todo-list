<template>
  <v-list class="pt-0" two-line flat>
    <v-text-field
      class="pa-4"
      @click:append="addTask"
      v-on:keyup.enter="addTask"
      outlined
      label="Add Task"
      append-icon="mdi-plus"
      hide-details
      clearable
      v-model="newTaskTitle"
    ></v-text-field>
    <div v-for="task in tasks" :key="task.id">
      <v-list-item
        :class="{ 'blue lighten-5': task.done }"
        @click="doneTask(task.id)"
      >
        <template v-slot:default>
          <v-list-item-action>
            <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title
              :class="{ 'text-decoration-line-through': task.done }"
              >{{ task.title }}</v-list-item-title
            >
          </v-list-item-content>
          <v-list-item-action>
            <v-btn icon @click.stop="deleteTask(task.id)">
              <v-icon color="red">mdi-delete</v-icon>
            </v-btn>
          </v-list-item-action>
        </template>
      </v-list-item>
      <v-divider></v-divider>
    </div>
  </v-list>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      newTaskTitle: "",
      tasks: [
        // {
        //   id: 1,
        //   title: "Wake Up",
        //   done: false,
        // },
        // {
        //   id: 2,
        //   title: "Get Fruits",
        //   done: false,
        // },
        // {
        //   id: 3,
        //   title: "Eat Fruits",
        //   done: false,
        // },
      ],
    };
  },
  methods: {
    doneTask(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    addTask() {
      let newTask = {
        id: Date.now(),
        title: this.newTaskTitle,
        done: false,
      }
      this.tasks.push(newTask)
      this.newTaskTitle = ''
    },
  },

  components: {},
};
</script>
