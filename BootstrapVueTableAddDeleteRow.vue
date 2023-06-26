<template>
  <div>
    <b-row class="mt-4">
      <b-col cols="12">
        <b-table class="workout-table" :items="items" :fields="fields">
          <template #head(add)="data">
            <b-link href="#">
              <b-icon class="workout-icon" icon="plus-circle" scale="1.5"
                      @click="addExerciseRow"></b-icon>
            </b-link>
          </template>

          <template #cell(add)="row">
            <b-link href="#">
              <b-icon class="workout-icon mt-2" icon="x-circle" scale="1.5"
                      @click="deleteExerciseRow(row.index)"></b-icon>
            </b-link>
          </template>

          <template #cell(exercise)="data">
            <b-form-select v-model="data.item.selectedExercise">
              <option v-for="(exercise, index) in exercises" :value="exercise.exerciseID" :key="index">
                {{ exercise.exerciseName }}
              </option>
            </b-form-select>
          </template>

          <template #cell(sets)="data">
            <b-form-input type="number">
            </b-form-input>
          </template>

          <template #cell(volume)="data">
            <b-form-input type="number">
            </b-form-input>
          </template>

          <template #cell(target)="data">
            <b-form-input type="number">
            </b-form-input>
          </template>

          <template #cell(rest)="data">
            <b-form-input type="text" v-model="data.item.restTime" placeholder="mm:ss"
                          @input="validateRestTime(data)">
            </b-form-input>
            <span v-if="!data.item.validRestTime" style="color: #EA4C89; font-size: 14px;">Time invalid</span>
          </template>
        </b-table>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "BootstrapVueTableAddDeleteRow",
  data() {
    return {
      exercises: [
        {exerciseID: 1, exerciseName: "Exercise1"},
        {exerciseID: 2, exerciseName: "Exercise2"},
        {exerciseID: 3, exerciseName: "Exercise3"},
      ],
      fields: [
        {key: 'add', label: ''},
        {key: 'exercise', label: 'Exercise'},
        {key: 'sets', label: 'Sets'},
        {key: 'volume', label: 'Volume'},
        {key: 'target', label: 'Target'},
        {key: 'rest', label: 'Rest'},
      ],
      items: [],
      selectedExercise: null,
      restTime: "",
    };
  },
  methods: {
    addExerciseRow() {
      this.workoutTableItems.push({
        exercise: '',
        sets: '',
        volume: '',
        target: '',
        rest: '',
        validRestTime: true,
      });
    },
    deleteExerciseRow(index) {
      this.workoutTableItems.splice(index, 1);
    },
    validateRestTime(data) {
      const rest = data.item.restTime;
      if (rest?.includes(":")) {
        const time = rest.split(":");
        if (time.length === 2) {
          const minutes = time[0];
          const seconds = time[1];
          let isMinutesNum = /^\d+$/.test(minutes);
          let isSecondsNum = /^\d+$/.test(seconds);
          if (isMinutesNum && isSecondsNum && minutes.length === 2 && seconds.length === 2) {
            data.item.validRestTime = seconds >= 0 && seconds < 59;
            return;
          }
        }
      }
      data.item.validRestTime = false;
    }
  },
}
</script>

<style>
/* Add your styles here */
</style>
