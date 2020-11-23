<template>
  <div>
    <p>{{ currentMonth + ' ' + currentDayofMonth + ' ' + currentYear}}</p>
    <div>
      <CalendarDay 
        v-for="day in daysInMonth" 
        :key="day" 
        :day="day"
      />
    </div>
  </div>
</template>

<script>
import moment from 'moment';
import CalendarDay from './CalendarDay';

export default {
  components: {
    CalendarDay
  },
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