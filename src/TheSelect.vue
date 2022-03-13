<template>
  <div>
    <h1>The Select</h1>

    <div>
      <h4>Selected ({{ Object.keys(selected).length }})</h4>
      <div v-if="Object.keys(selected).length">
        <span @click="unselect(index)" v-for="(item, index) in selected" :key="index" class="badge rounded-pill bg-success">{{ index }}: {{ item }}</span>
      </div>
    </div>

    <div>
      <h4>Items ({{ Object.keys(items).length }})</h4>
      <div v-if="Object.keys(items).length">
        <span @click="select(index)" v-for="(item, index) in items" :key="item.id" class="badge rounded-pill bg-primary">{{ index }}: {{ item }}</span>
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
    initialItems: {
      type: Object,
      default: {}
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
      this.selected.index = this.items[index]
      delete this.items[index]
    },
    unselect(index) {
      this.items.push(this.selected[index])
      delete this.selected[index]
    }
  },

  mounted() {
    this.items = this.initialItems
  }
}
</script>
