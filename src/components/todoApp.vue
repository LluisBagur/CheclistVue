<template>
  <v-container>
    <v-row class="text-center" justify="center">
      <v-col cols="12">
        <v-container>
          <v-row justify="center">
            <v-col cols="12" md="4">
              <v-text-field
                v-model.trim="newTodoContent"
                :counter="25"
                label="Task Name:"
                required
                @input="activateButton"
                @blur="desactivateButton"
              ></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-btn color="primary" class="mr-4" @click="addTask">
                Add
              </v-btn>
            </v-col>
          </v-row>
        </v-container>
      </v-col>
      <v-col cols="12">
        <todoList
          v-bind:items="todoItems"
          :Chekfunction="handleCheck"
          :deleteFunction="removeTask"
        ></todoList>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import todoList from "./todoList";

export default {
  name: "HelloWorld",
  components: { todoList },

  data: () => ({
    validButton: false,
    newTodoContent: "",
    todoItems: []
  }),
  methods: {
    activateButton() {
      this.validButton = true;
    },
    desactivateButton() {
      this.validButton = false;
    },
    addTask() {
      if (!this.newTodoContent) return;
      // añadido nuevo item al array
      this.todoItems.push({
        id: Math.random()
          .toString(36)
          .substr(2, 9),
        content: this.newTodoContent,
        createdAt: Date.now(),
        checked: false,
        completedAt: null
      });
      // eliminamos el input para el siguiente
      this.newTodoContent = "";
      console.log(this.todoItems);
    },
    removeTask(id) {
      this.todoItems.map(item => {
        if (item.id === id) {
          this.todoItems.splice(this.todoItems.indexOf(item), 1);
        }
      });
    },
    handleCheck(id) {
      this.todoItems.map(item => {
        if (item.id === id) {
          item.checked = !item.checked;
        }
      });
    }
  }
};
</script>
