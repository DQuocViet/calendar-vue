<template>
  <div id="calendar-entry">
    <div class="calendar-entry-note">
      <input type="text" class="input-event" placeholder="New Event" v-model="inputEntry" required/>
      <p class="calendar-entry-day">
        Day of event: <span class="bold">{{ titleOfActiveDay }}</span></p>
      <a class="button is-primary is-small is-outlined" @click="submitEvent(inputEntry)">
        Submit
      </a>
    </div>
    <p style="color: red; font-size: 13px" v-if="error"> You must type something first! </p>
  </div>
</template>
<script>
import {store} from '@/store';

export default {
  name: 'CalendarEntry',
  data() {
    return {
      inputEntry: '', error: false
    }
  },
  computed: {
    titleOfActiveDay() {
      return store.getActiveDay().fullTitle;
    }
  },
  methods: {
    submitEvent(eventDetails) {
      if (eventDetails === '') return this.error = true;
      store.submitEvent(eventDetails);
      this.inputEntry = '';
      this.error = false;
    }
  }
} </script>
<style lang="scss" scoped>
#calendar-entry {
  background-color: white;
  border: solid 1px #85deb0;
  border-radius: 5px;
  padding: 20px;
}

.input-event {
  border-top: 0;
  border-right: 0;
  border-left: 0;
  border-bottom: solid 1px #ccc;
}

.button.is-primary.is-small.is-outlined {
  border-radius: 3px;
  border: solid 2px #85deb0;
  font-size: 14px;
  padding: 5px;
  color: #85deb0;
}
.calendar-entry-day {
  color: #85deb0;
  font-size: 14px;
}
</style>