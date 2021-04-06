<template>
  <div v-bind:class="[editMode ? 'day editMode' : 'day']">
    <div v-bind:class="[isToday ? 'day-badge today' : 'day-badge']">
      {{ day }}
    </div>
    <span
      v-if="!editMode && !(creditTotal > 0 || debitTotal > 0)"
      class="small-itals mx-4"
    >
      To add a payment, click "edit"
    </span>
    <div
      v-if="!editMode && (creditTotal > 0 || debitTotal > 0)"
      class="total-content positive"
    >
      <svg
        class="w-6 h-6"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M5 15l7-7 7 7"
        ></path>
      </svg>
      {{ formatMoney(creditTotal) }}
    </div>
    <span
      v-if="!editMode && (creditTotal > 0 || debitTotal > 0)"
      class="total-content negative"
    >
      <svg
        class="w-6 h-6"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M19 9l-7 7-7-7"
        ></path>
      </svg>
      {{ formatMoney(debitTotal) }}
    </span>
    <div v-if="editMode" class="edit-container">
      <div class="list-container">
        <ul>
          <li
            v-for="(credit, i) in credits"
            :key="`c-${day}-${i}`"
            class="positive"
          >
            + {{ formatMoney(credit) }}
            <!-- <button class="small-itals" v-on:click="removeEntry('credits', credit)">(remove)</button> -->
          </li>
        </ul>
        <form class="horiz-form" @submit.prevent="onSubmitCredit">
          <input v-model.number="newCredit" placeholder="Add money coming in" />
          <input class="small-submit" type="submit" value="+" />
        </form>
      </div>
      <div class="list-container">
        <ul>
          <li
            v-for="(debit, i) in debits"
            :key="`d-${day}-${i}`"
            class="negative"
          >
            - {{ formatMoney(debit) }}
            <!-- <button class="small-itals" v-on:click="removeEntry('debits', debit)">(remove)</button> -->
          </li>
        </ul>
        <form class="horiz-form" @submit.prevent="onSubmitDebit">
          <input v-model.number="newDebit" placeholder="Add money going out" />
          <input class="small-submit" type="submit" value="+" />
        </form>
      </div>
    </div>
    <button v-on:click="toggleEditMode" class="edit-btn">
      {{ !editMode ? "Edit" : "Close" }}
    </button>
  </div>
</template>

<script>
import { Money } from "../mixins/formatMoney";

export default {
  mixins: [Money],
  props: {
    day: {
      type: Number,
      required: true,
    },
    isToday: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      debits: [],
      credits: [],
      editMode: false,
      newDebit: null,
      newCredit: null,
    };
  },
  methods: {
    pushUpdatesToParent() {
      const payload = { day: this.day, total: this.dayTotal };
      this.$emit("submit-day", payload);
    },
    toggleEditMode() {
      let old = this.editMode;
      if (old) {
        this.pushUpdatesToParent();
      }
      this.editMode = !old;
    },
    onSubmitCredit() {
      if (this.newCredit !== null && !isNaN(this.newCredit)) {
        this.credits.push(this.newCredit);
      }
      this.newCredit = null;
    },
    onSubmitDebit() {
      if (this.newDebit !== null && !isNaN(this.newDebit)) {
        this.debits.push(this.newDebit);
      }
      this.newDebit = null;
    },
    removeEntry(arrayName, val) {
      const ind = this[arrayName].indexOf(val);
      if (ind > -1) {
        this[arrayName].splice(ind, 1);
      }
    },
  },
  computed: {
    creditTotal() {
      if (this.credits.length === 0) {
        return 0;
      }
      return this.credits.reduce((a, b) => a + b, 0);
    },
    debitTotal() {
      if (this.debits.length === 0) {
        return 0;
      }
      return this.debits.reduce((a, b) => a + b, 0);
    },
    dayTotal() {
      return this.creditTotal - this.debitTotal;
    },
  },
};
</script>

<style scoped>
.day {
  @apply flex items-center justify-between rounded-full py-3 px-4 my-4 mx-2;
  background-color: #e7eee8;
}
.day.editMode {
  @apply rounded-none mx-0 flex-col xl:flex-row;
}
.day-badge {
  @apply rounded-full h-12 w-12 flex items-center justify-center bg-white text-2xl font-bold px-4;
  color: #83058a;
}
.day-badge.today {
  color: #54785a !important;
}
.total-content {
  @apply text-lg font-medium flex items-center justify-center;
}
.small-itals {
  @apply text-sm italic;
}
.positive {
  @apply text-green-700;
}
.negative {
  @apply text-red-700;
}
.edit-btn {
  @apply flex items-center justify-between rounded-full py-3 px-4 bg-white;
}
.small-submit {
  @apply w-full flex items-center justify-center px-1 py-2 border border-transparent text-base font-medium rounded-md text-white;
  color: #83058a;
}
.edit-container {
  @apply flex flex-col items-center justify-center flex-wrap;
}
.edit-container div {
  @apply mx-4;
}
.edit-container ul,
form {
  @apply pb-4;
}
.horiz-form {
  @apply flex;
}
.horiz-form input {
  @apply px-2 py-1 border border-transparent placeholder-gray-500 focus:ring-offset-2 sm:max-w-xs rounded-md;
}
</style>
