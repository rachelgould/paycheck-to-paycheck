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
    },
    credits: {
      type: Number,
      required: false
    },
    debits: {
      type: Number,
      required: false
    },
  },
};
</script>