<template>
  <div>
    <p>{{ day }}</p>
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
};
</script>