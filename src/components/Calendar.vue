<template>
  <SummaryStats :outstandingTotal="outstandingTotal" />
  <div class="container mx-auto bg-green rounded-2xl w-11/12 lg:w-2/3 xl:w-2/3">
    <h1 class="purple text-3xl text-center pt-12 font-bold">
      {{ currentMonth + ' ' + currentYear}}
    </h1>
    <div class="md:p-8 lg:p-8 xl:p-8">
      <CalendarDay 
        @submit-day="submitDayTotal"
        v-for="day in daysInMonth" 
        :key="day" 
        :day="day"
        :isToday="isToday(day)"
      />
    </div>
  </div>
</template>

<script>
import moment from 'moment';
import CalendarDay from './CalendarDay';
import SummaryStats from './SummaryStats';

export default {
  components: {
    CalendarDay,
    SummaryStats
  },
  data() {
    return {
      outstandingTotal: 0
    }
  },
  methods: {
    currentDateTime() {
      return moment().format('MMMM Do YYYY, h:mm:ss a')
    },
    isToday(day) {
      return Number(moment().format('DD')) === Number(day);
    },
    submitDayTotal({ day, total }) {
      if (day >= this.currentDayofMonth) {
        this.outstandingTotal += total;
      }
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