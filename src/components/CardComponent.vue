<template>
  <div class="card">
    <div class="card-content">
      <slot/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardComponent',
  props: {
    title: {
      type: String,
      default: null
    },
    icon: {
      type: String,
      default: null
    },
    headerIcon: {
      type: String,
      default: null
    }
  },
  methods: {
    headerIconClick () {
      this.$emit('header-icon-click')
    }
  }
}
</script>
