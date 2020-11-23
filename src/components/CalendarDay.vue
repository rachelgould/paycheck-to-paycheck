<template>
  <div v-bind:class="[editMode ? 'day-editMode' : 'day']">
    {{ day }} || 
    <span v-if="credits.length && !editMode">
      +{{ credits }}{{' '}}
    </span>
    <span v-if="debits.length && !editMode">
      -{{ debits }}{{' '}}
    </span>
    <div v-if="editMode">
      Credits:
      <ul>
        <li v-for="(credit, i) in credits" :key="`c-${day}-${i}`">
          {{credit}}
          <button>x</button>
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
          <button>x</button>
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
      this.credits.push(this.newCredit);
      this.newCredit = null;
    },
    onSubmitDebit() {
      this.debits.push(this.newDebit);
      this.newDebit = null;
    }
  }
};
</script>