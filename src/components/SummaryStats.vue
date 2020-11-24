<template>
  <div class="container mx-auto bg-green rounded-2xl w-11/12 lg:w-2/3 xl:w-2/3 mb-4 p-8">
    <h3 class="purple text-xl font-medium">
      How You're Doing This Month
    </h3>
    <dl class="mt-5 grid grid-cols-1 gap-5 sm:grid-cols-2">
      <div class="bg-lightgreen overflow-hidden shadow rounded-lg">
        <div class="px-4 py-5 sm:p-6">
          <dt class="text-sm font-medium purple">
            Money In Your Account Today
          </dt>
          <dd class="mt-1 text-3xl font-semibold text-gray-900">
            $ {{ inAccount ? inAccount : '?' }}
          </dd>
        </div>
      </div>

      <div class="bg-lightgreen overflow-hidden shadow rounded-lg">
        <div class="px-4 py-5 sm:p-6">
          <dt class="text-sm font-medium purple">
            What You'll Have Left
          </dt>
          <dd class="mt-1 text-3xl font-semibold text-gray-900">
            $ {{ leftOver }}
          </dd>
        </div>
      </div>
    </dl>
  </div>
</template>

<script>
export default {
  props: {
    totalFromEntered: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      inAccount: null
    }
  },
  computed: {
    leftOver() {
      const newTotal = this.inAccount + this.totalFromEntered;
      if (!isNaN) {
        return newTotal;
      }
      return '?';
    }
  }
}
</script>