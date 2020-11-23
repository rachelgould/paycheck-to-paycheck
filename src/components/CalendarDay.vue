<template>
  <div>
    {{ day }} || 
    <span v-if="credits.length">
      +{{ credits }}{{' '}}
    </span>
    <span v-if="debits.length">
      -{{ debits }}{{' '}}
    </span>
    <button>Add Credit</button>
    <button>Add Debit</button>
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
      credits: []
    }
  }
};
</script>