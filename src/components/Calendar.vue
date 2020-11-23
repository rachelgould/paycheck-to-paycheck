<template>
  <div>
    <p>{{currentDateTime()}}</p>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  methods: {
    currentDateTime() {
      return moment().format('MMMM Do YYYY, h:mm:ss a')
    }
  }
};
</script>