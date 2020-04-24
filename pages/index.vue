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
        <div v-for="goal in goals" :key="goal">{{goal}}</div>
      </b-col>
      <b-col sm="6">
        <h2>Tasks</h2>
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
      showGoals: true
    };
  },
  methods: {
    submitGoal() {
      this.goals.push(this.goalInput);
      this.goalInput = "";
    }
  },
  computed: {}
};
</script>

<style scoped>
</style>