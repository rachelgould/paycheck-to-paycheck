<template>
  <div class="container mx-auto mt-12 sm:px-1 md:4 px-8 mb-12">
    <img
      src="@/assets/images/Paycheck-logo.png"
      alt="simple budgeting"
      class="mx-auto mb-8"
    />
    <div
      class="text-center text-black mb-8 w-11/12 lg:w-2/3 xl:w-2/3 mx-auto text-black"
    >
      <h2 class="font-medium text-xl text-center mb-4">
        Wondering how much money you'll have at the end of the month?
      </h2>
      <p>
        <span class="font-medium">Tip:</span> Start by entering how much is in
        your account right now, and then fill in any payments or expenses for
        the remainder of the month.
      </p>
      <!-- <p class="font-medium">Adding credits/debits for days that have already passed will not affect your total, since they should be reflected in your current account total.</p> -->
    </div>
    <Calendar />
  </div>
</template>

<script>
import Calendar from "./components/Calendar.vue";

export default {
  name: "App",
  components: {
    Calendar,
  },
};
</script>
