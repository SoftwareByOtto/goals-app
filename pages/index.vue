<template>
  <b-container>
    <h1>
      Goals App
      <b-button @click="showGoals = !showGoals">Toggle Goals</b-button>
    </h1>
    <b-row>
      <b-col sm="6" v-if="showGoals">
        <h2>Goals</h2>
        <b-form @submit.prevent="submitGoal">
          <b-input-group>
            <b-input autofocus v-model="goalInput"></b-input>
            <template v-slot:append>
              <b-button type="submit">Submit</b-button>
            </template>
          </b-input-group>
        </b-form>
        <div v-for="goal in goals" :key="goal" @click="addTaskToGoal(goal)">{{goal}}</div>
      </b-col>
      <b-col sm="6">
        <h2>Tasks</h2>
        <div v-for="task in tasks" :key="task">
          <b-form-group :description="task.goal">
            <b-input v-model="task.task"></b-input>
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
      tasks: []
    };
  },
  methods: {
    submitGoal() {
      this.goals.push(this.goalInput);
      this.goalInput = "";
    },
    addTaskToGoal(goal) {
      this.tasks.push({
        task: "",
        goal
      });
    }
  },
  computed: {}
};
</script>

<style scoped>
</style>