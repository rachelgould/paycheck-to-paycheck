<template>
  <div>
    <p>{{ currentMonth + ' ' + currentDayofMonth + ' ' + currentYear}}</p>
    <div>
      <CalendarDay 
        v-for="day in daysInMonth" 
        :key="day" 
        :day="day"
        :debits="entries[day]['debits']"
        :credits="entries[day]['credits']"
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
  data() {
    return {
      entries: {
        1: {
          debits: [],
          credits: []
        },
        2: {
          debits: [],
          credits: []
        },
        3: {
          debits: [],
          credits: []
        },
        4: {
          debits: [],
          credits: []
        },
        5: {
          debits: [],
          credits: []
        },
        6: {
          debits: [],
          credits: []
        },
        7: {
          debits: [],
          credits: []
        },
        8: {
          debits: [],
          credits: []
        },
        9: {
          debits: [],
          credits: []
        },
        10: {
          debits: [],
          credits: []
        },
        11: {
          debits: [],
          credits: []
        },
        12: {
          debits: [],
          credits: []
        },
        13: {
          debits: [],
          credits: []
        },
        14: {
          debits: [],
          credits: []
        },
        15: {
          debits: [],
          credits: []
        },
        16: {
          debits: [],
          credits: []
        },
        17: {
          debits: [],
          credits: []
        },
        18: {
          debits: [],
          credits: []
        },
        19: {
          debits: [],
          credits: []
        },
        20: {
          debits: [],
          credits: []
        },
        21: {
          debits: [],
          credits: []
        },
        22: {
          debits: [],
          credits: []
        },
        23: {
          debits: [],
          credits: []
        },
        24: {
          debits: [],
          credits: []
        },
        25: {
          debits: [],
          credits: []
        },
        26: {
          debits: [],
          credits: []
        },
        27: {
          debits: [],
          credits: []
        },
        28: {
          debits: [],
          credits: []
        },
        29: {
          debits: [],
          credits: []
        },
        30: {
          debits: [],
          credits: []
        },
        31: {
          debits: [],
          credits: []
        }
      }
    }
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