<template>
  <b-container>
    <h1>
      Goals App
      <b-button @click="showGoals = !showGoals">{{showGoals ? 'Hide' : 'Show'}} Goals</b-button>
      <b-button
        @click="showArchivedGoals = !showArchivedGoals"
      >{{showArchivedGoals ? 'Hide' : 'Show'}} Archived Goals</b-button>
      <b-button
        @click="showCompletedTasks = !showCompletedTasks"
      >{{showCompletedTasks ? 'Hide' : 'Show'}} Completed Tasks</b-button>
    </h1>
    <b-row>
      <b-col md v-if="showGoals">
        <h2>Goals</h2>
        <b-form @submit.prevent="submitGoal">
          <b-input-group>
            <b-input required autofocus v-model="goalInput"></b-input>
            <template v-slot:append>
              <b-button type="submit">Submit</b-button>
            </template>
          </b-input-group>
        </b-form>
        <b-card
          class="mt-2"
          v-for="goal in filteredGoals"
          :key="goal"
          @click="addTaskToGoal(goal)"
          @click.right.prevent="toggleArchiveGoal(goal)"
        >
          <b-card-title>
            {{goal.goal}}
            <b-badge v-if="goal.archived">Archived</b-badge>
          </b-card-title>
        </b-card>
      </b-col>
      <b-col md>
        <h2>Tasks</h2>
        <div v-for="task in incompleteTasks" :key="task">
          <b-form @submit.prevent="completeTask(task)">
            <b-form-group :description="task.goal">
              <b-input-group>
                <b-input v-model="task.task"></b-input>
                <template v-slot:append>
                  <b-button type="submit">Complete</b-button>
                </template>
              </b-input-group>
            </b-form-group>
          </b-form>
        </div>
      </b-col>
      <b-col md v-if="showCompletedTasks">
        <h2>Completed Tasks</h2>
        <div v-for="task in completeTasks" :key="task">
          <b-form-group :description="task.goal">
            <b-input disabled v-model="task.task"></b-input>
          </b-form-group>
        </div>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import { mapState, mapMutations, mapActions } from "vuex";
export default {
  data() {
    return {
      goals: [],
      goalInput: "",
      showGoals: true,
      showCompletedTasks: false,
      showArchivedGoals: false,
      tasks: []
    };
  },
  methods: {
    submitGoal() {
      this.goals.push({
        goal: this.goalInput,
        archived: false
      });
      this.goalInput = "";
    },
    addTaskToGoal(goal) {
      this.tasks.push({
        task: "",
        goal: goal.goal,
        complete: false
      });
    },
    completeTask(task) {
      task.complete = true;
    },
    toggleArchiveGoal(goal) {
      goal.archived = !goal.archived;
    }
  },
  computed: {
    incompleteTasks() {
      return this.tasks.filter(task => task.complete === false);
    },
    completeTasks() {
      return this.tasks.filter(task => task.complete === true);
    },
    filteredGoals() {
      if (this.showArchivedGoals) {
        return this.goals;
      } else {
        return this.goals.filter(goal => goal.archived === false);
      }
    }
  }
};
</script>

<style scoped>
</style>