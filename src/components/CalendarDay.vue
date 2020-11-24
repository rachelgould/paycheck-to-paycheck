<template>
  <div v-bind:class="[editMode ? 'day editMode' : 'day']">
    <div v-bind:class="[isToday ? 'day-badge today' : 'day-badge']">
      {{ day }}
    </div>
    <span
      v-if="!editMode && !(creditTotal > 0 || debitTotal > 0)"
      class="total-nocontent">
      To add a payment, click "edit"
    </span>
    <div 
      v-if="!editMode && (creditTotal > 0 || debitTotal > 0)" 
      class="total-content positive">
       <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 15l7-7 7 7"></path></svg> {{ creditTotal }}
    </div>
    <span 
      v-if="!editMode && (creditTotal > 0 || debitTotal > 0)" 
      class="total-content negative">
      <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path></svg> {{ debitTotal }}
    </span>
    <div v-if="editMode">
      Credits:
      <ul>
        <li v-for="(credit, i) in credits" :key="`c-${day}-${i}`">
          {{credit}}
          <button v-on:click="removeEntry('credits', credit)">x</button>
        </li>
      </ul>
      <form @submit.prevent="onSubmitCredit">
        <input v-model.number="newCredit">
        <input class="button" type="submit" value="Submit"> 
      </form>
    </div>
    <div v-if="editMode">
      Debits:
      <ul>
        <li v-for="(debit, i) in debits" :key="`d-${day}-${i}`">
          {{debit}}
          <button v-on:click="removeEntry('debits', debit)">x</button>
        </li>
      </ul>
      <form @submit.prevent="onSubmitDebit">
        <input v-model.number="newDebit">
        <input class="button" type="submit" value="Submit"> 
      </form>
    </div>
    <button v-on:click="toggleEditMode">
      {{!editMode ? 'Edit' : 'Close'}}
    </button>
  </div>
</template>

<script>

export default {
  props: {
    day: {
      type: Number,
      required: true
    },
    isToday: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      debits: [],
      credits: [],
      editMode: false,
      newDebit: null,
      newCredit: null
    }
  },
  methods: {
    toggleEditMode() {
      let old = this.editMode;
      this.editMode = !old;
    },
    onSubmitCredit() {
      if (!isNaN(this.newCredit)) {
        this.credits.push(this.newCredit);
      }
      this.newCredit = null;
    },
    onSubmitDebit() {
      if (!isNaN(this.newDebit)) {
        this.debits.push(this.newDebit);
      }
      this.newDebit = null;
    },
    removeEntry(arrayName, val) {
      const ind = this[arrayName].indexOf(val);
      if (ind > -1) {
        this[arrayName].splice(ind, 1);
      }
    }
  },
  computed: {
    creditTotal() {
      return this.credits.reduce((a, b) => (a+b), 0);
    },
    debitTotal() {
      return this.debits.reduce((a, b) => (a+b), 0);
    }
  }
};
</script>

<style scoped>
  .day {
    @apply flex items-center justify-between rounded-full py-3 px-4 my-4;
    background-color: #E7EEE8;
  }
  .day-badge {
    @apply rounded-full h-12 w-12 flex items-center justify-center bg-white text-2xl font-bold;
    color: #83058A;
  }
  .day-badge.today {
    color: #54785A !important;
  }
  .total-content {
    @apply text-lg font-medium flex items-center justify-center;
  }
  .total-nocontent {
    @apply text-sm italic
  }
  .positive {
    @apply text-green-700;
  }
  .negative {
    @apply text-red-700;
  }
</style>