<template>
  <div :class="this.getClass()" role="alert">
    <div class="hstack gap-2">
      <span>
        <Icon v-if="this.autorefresh" icon="spinner" fixed-width spin size="lg" />
        <Icon v-else :icon="icon" fixed-width size="lg" />
      </span>
      <div>
        <span>{{ message }}</span>
        <span v-if="autorefresh" class="d-block">Prehliadač sa automaticky obnoví o {{ seconds }} sekúnd</span>
      </div>
    </div>
    <button v-if="this.dismissible" type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
  </div>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'primary',
      validator: function (value) {
        return [
          'primary',
          'danger',
          'success',
          'warning'
        ].indexOf(value) !== -1
      }
    },
    icon: {
      type: String,
      default: 'info-circle'
    },
    dismissible: {
      type: Boolean,
      default: true
    },
    autorefresh: {
      type: Boolean,
      default: false
    }
  },

  data() {
    return {
      seconds: 30,
      interval: null
    }
  },

  mounted() {
    if (this.autorefresh) {
      this.startCountdown()
      this.interval = setInterval(this.decrement, 1000)
    }
  },

  methods: {
    decrement() {
      if (this.seconds === 1) {
        clearInterval(this.interval)
      } else {
        this.seconds--
      }
    },

    getClass() {
      let classes = [];

      classes.push('alert')
      classes.push(`alert-${this.type}`)

      if (this.dismissible) {
        classes.push('alert-dismissible')
      }

      classes.push('fade show')

      return classes.join(' ')
    },

    startCountdown() {
      setTimeout(() => {
        document.location.reload(true)
      }, this.seconds * 1000);
    }
  },
}
</script>
