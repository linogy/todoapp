<template>
  <q-page class="q-ma-md">
    <div class="row q-mb-lg">
      <search />
    </div>

    <no-tasks v-if="!Object.keys(tasksTodo).length"></no-tasks>
    <tasks-todo v-else :tasksTodo="tasksTodo" />
    <tasks-completed v-if="Object.keys(tasksCompleted).length" :tasksCompleted="tasksCompleted" />
    <div class="absolute-bottom text-center q-mb-lg">
      <q-btn @click="showAddTask = true" round color="primary" size="24px" icon="add" />
    </div>
    <q-dialog v-model="showAddTask">
      <add-task @close="showAddTask = false"></add-task>
    </q-dialog>
  </q-page>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  data() {
    return {
      showAddTask: false,
    };
  },
  computed: {
    ...mapGetters("tasks", ["tasksTodo", "tasksCompleted"]),
  },
  components: {
    task: require("components/Tasks/Task.vue").default,
    "add-task": require("components/Tasks/Modals/addTask.vue").default,
    "tasks-todo": require("components/Tasks/Modals/TasksTodo.vue").default,
    "tasks-completed": require("components/Tasks/Modals/TasksCompleted.vue")
      .default,
    "no-tasks": require("components/Tasks/Modals/NoTasks.vue").default,
    search: require("components/Tasks/Tools/Search.vue").default,
  },
  mounted() {
    this.$root.$on("showAddTask", () => {
      this.showAddTask = true;
    });
  },
};
</script>

<style lang="scss" scoped></style>
