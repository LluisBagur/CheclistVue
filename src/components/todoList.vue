<template>
  <v-card
    :elevation="hover ? 12 : 2"
    class="mx-auto"
    height="auto"
    max-width="450"
  >
    <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-center">Task</th>
            <th class="text-center">Done?</th>
            <th class="text-center">Remove</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in items" :key="item.id">
            <td>{{ item.content }}</td>
            <td>
              <input
                type="checkbox"
                v-bind:checked="item.checked"
                @change="executeCheck(item.id)"
              />
            </td>
            <td>
              <v-icon color="primary" @click="executeRemove(item.id)" dark
                >mdi-delete</v-icon
              >
            </td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </v-card>
</template>

<script>
/**
 * @module TodoItem
 */
export default {
  name: "TodoList",
  props: {
    /**
     *  @type TodoItem
     */
    items: {
      type: Object,
      required: true
    },
    Chekfunction: {
      type: Function
    },
    deleteFunction: {
      type: Function
    }
  },
  data() {
    return {
      isEditing: false,
      contentLocal: ""
    };
  },

  methods: {
    executeCheck(id) {
      if (this.Chekfunction) {
        this.Chekfunction(id);
      }
    },
    executeRemove(id) {
      if (this.deleteFunction) {
        this.deleteFunction(id);
      }
    }
  }
};
</script>
