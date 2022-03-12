<template>
  <button :class="buttonClass" @click="handleClick">
    <icon v-if="loading" icon="spinner" spin />
    <slot v-else></slot>
  </button>
</template>

<script>
export default {
  props: {
    initialLoading: {
      type: Boolean,
      default: false
    },
    type: {
      type: String,
      default: 'primary'
    },
    outline: {
      type: Boolean,
      default: false
    }
  },

  data() {
    return {
      loading: null
    }
  },

  computed: {
    buttonClass() {
      return this.outline ? `btn btn-outline-${this.type}` : `btn btn-${this.type}`
    }
  },

  methods: {
    handleClick() {
      this.$emit('clicked')
    },
    toggleLoading() {
      if (this.loading) {
        this.loading = false
      } else {
        this.loading = true
      }
    }
  },

  mounted() {
    this.loading = this.initialLoading
  }

}
</script>
