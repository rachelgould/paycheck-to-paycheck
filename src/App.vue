<template>
  <div class="container mx-auto mt-12 px-8">
    <img src="@/assets/images/Paycheck-logo.png" alt="simple budgeting" class="mx-auto mb-8">
    <div class="text-center mb-8">
      <h2 class="darkgreen font-medium text-xl text-center mb-4">
        Wondering how much money you'll have at the end of the month?
      </h2>
      <p class="darkgreen"><span class="font-medium">Tip:</span> Start by entering how much is in your account right now, and then fill in any payments or expenses for the remainder of the month.</p>
    </div>
    <Calendar />
  </div>
</template>

<script>
import Calendar from './components/Calendar.vue'

export default {
  name: 'App',
  components: {
    Calendar
  }
}
</script>
