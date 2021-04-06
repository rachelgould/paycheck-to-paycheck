<template>
  <div
    class="container mx-auto bg-green rounded-2xl w-11/12 lg:w-2/3 xl:w-2/3 mb-4 p-8"
  >
    <h3 class="purple text-xl font-medium">
      How You're Doing This Month
    </h3>
    <dl class="mt-5 grid grid-cols-1 gap-5 sm:grid-cols-2">
      <div class="bg-lightgreen overflow-hidden shadow rounded-lg">
        <div class="px-4 py-5 sm:p-6">
          <dt class="text-md font-medium purple">
            Money In Your Account Today
          </dt>
          <dd
            v-if="!editMode"
            class="mt-1 py-4 text-md font-medium text-gray-900"
          >
            {{
              inAccount ? formatMoney(inAccount) : "Add your current balance"
            }}
          </dd>
          <form
            class="mt-2 flex flex-col xl:flex-row"
            v-if="editMode"
            @submit.prevent="onSubmit"
          >
            <input
              v-model.number="inAccount"
              placeholder="Enter a new amount"
            />
            <input class="small-submit" type="submit" value="Submit" />
          </form>
          <button
            v-if="!editMode"
            v-on:click="toggleEditMode"
            class="text-sm italic"
          >
            {{ !editMode ? "(Edit)" : "Close" }}
          </button>
        </div>
      </div>

      <div class="bg-lightgreen overflow-hidden shadow rounded-lg">
        <div class="px-4 py-5 sm:p-6">
          <dt class="text-md font-medium purple">
            What You'll Have Left
          </dt>
          <dd class="mt-1 py-4 text-md font-medium text-gray-900">
            {{ leftOver ? formatMoney(leftOver) : "" }}
          </dd>
        </div>
      </div>
    </dl>
  </div>
</template>

<script>
import { Money } from "../mixins/formatMoney";

export default {
  props: {
    outstandingTotal: {
      type: Number,
      required: true,
    },
  },
  mixins: [Money],
  data() {
    return {
      inAccount: null,
      editMode: false,
    };
  },
  methods: {
    toggleEditMode() {
      let old = this.editMode;
      this.editMode = !old;
    },
    onSubmit() {
      this.toggleEditMode();
    },
  },
  computed: {
    leftOver() {
      const newTotal = Number(this.inAccount) + Number(this.outstandingTotal);
      if (this.inAccount && !isNaN(newTotal)) {
        return newTotal;
      }
      return null;
    },
  },
};
</script>

<style scoped>
.small-submit {
  @apply w-full flex items-center justify-center px-1 py-2 border border-transparent text-base font-medium rounded-md text-white;
  color: #83058a;
}
input {
  @apply px-2 py-1 border border-transparent placeholder-gray-500 focus:ring-offset-2 sm:max-w-xs rounded-md;
}
</style>
