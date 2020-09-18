<template>
  <div>
    <q-item
      @click="updateTask({ id: id, updates: { completed: !task.completed } })"
      :class="!task.completed ? 'bg-orange-1' : 'bg-green-1'"
      clickable
    >
      <q-item-section side top>
        <q-checkbox v-model="task.completed" />
      </q-item-section>

      <q-item-section>
        <q-item-label :class="{ 'text-strikethrough': task.completed }">{{ task.name }}</q-item-label>
      </q-item-section>

      <q-item-section v-if="task.dueDate" side>
        <div class="row">
          <div class="column justify-center">
            <q-icon name="event" size="18px" class="q-mr-xs" />
          </div>

          <div class="column">
            <q-item-label class="row justify-end" caption>{{ task.dueDate }}</q-item-label>
            <q-item-label class="row justify-end" caption>
              <small>{{ task.dueTime }}</small>
            </q-item-label>
          </div>
        </div>
      </q-item-section>
      <q-item-section side>
        <div class="row">
          <q-btn @click.stop="showEditTask = true" flat round color="primary" icon="edit"></q-btn>
          <q-btn @click.stop="promptToDelete(id)" flat round color="red" icon="delete"></q-btn>
        </div>
      </q-item-section>

      <q-dialog v-model="showEditTask">
        <edit-task @close="showEditTask = false" :task="task" :id="id">Edit Task</edit-task>
      </q-dialog>
    </q-item>
  </div>
</template>

<script>
import { mapActions } from "vuex";

export default {
  data() {
    return {
      showEditTask: false,
    };
  },
  props: ["task", "id"],
  methods: {
    ...mapActions("tasks", ["updateTask", "deleteTask"]),
    promptToDelete(id) {
      this.$q
        .dialog({
          title: "Confirm",
          message: "Really delete?",
          cancel: {
            color: "negative",
          },
          persistent: true,
        })
        .onOk(() => {
          this.deleteTask(id);
        });
    },
  },
  components: {
    "edit-task": require("components/Tasks/Modals/EditTask.vue").default,
  },
};
</script>

<style></style>
