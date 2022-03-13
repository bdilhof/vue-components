<template>
  <div>
    <h1>The Select</h1>
    <div>
      <h4>Selected ({{ Object.keys(selected).length }})</h4>
      <pre>{{ this.selected }}</pre>
    </div>
    <div>
      <h4>Items ({{ Object.keys(items).length }})</h4>
      <div v-if="Object.keys(items).length">
        <span @click="select(index)" v-for="(item, index) in items" :key="item.id" class="badge rounded-pill bg-primary"><b>{{ index }}</b> <i>{{ item }}</i></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    open: {
      type: Boolean,
      default: false
    },
    multiple: {
      type: Boolean,
      default: false
    },
    options: {
      type: Object,
      default: function() {
        return {}
      }
    },
  },

  data() {
    return {
      items: {},
      selected: {}
    }
  },

  methods: {
    select(index) {
      let tempSelected = this.selected
      tempSelected[index] = this.items[index]

      this.selected = {}
      this.selected = tempSelected
    },
    unselect(index) {

    }
  },

  mounted() {
    this.items = this.options
  }
}
</script>
