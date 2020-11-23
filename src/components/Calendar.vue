<template>
  <div>
    <p>{{ currentMonth + ' ' + currentDayofMonth + ' ' + currentYear}}</p>
    <ul>
      <li v-for="day in daysInMonth" :key="day">
        {{day}}
      </li>
    </ul>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  methods: {
    currentDateTime() {
      return moment().format('MMMM Do YYYY, h:mm:ss a')
    }
  },
  computed: {
    currentMonth() {
      return moment().format('MMMM');
    },
    currentYear() {
      return moment().format('YYYY');
    },
    currentDayofMonth() {
      return moment().format('DD');
    },
    daysInMonth() {
      return moment().daysInMonth();
    }
  }
};
</script>