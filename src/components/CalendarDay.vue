<template>
  <div>
    {{ day }} || 
    <span v-if="credits.length">
      +{{ credits }}{{' '}}
    </span>
    <span v-if="debits.length">
      -{{ debits }}{{' '}}
    </span>
    <button v-on:click="toggleEditMode">
      {{!editMode ? 'Edit' : 'Save'}}
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
      editMode: false
    }
  },
  methods: {
    toggleEditMode() {
      let old = this.editMode;
      this.editMode = !old;
    }
  }
};
</script>