<template>
  <!-- Use this slot to set the header caption -->
  <div class="c-grid-column"><slot /></div>
</template>

<script>
import ColumnMixin from './c-grid/ColumnMixin.vue'
import StdColumnMixin from './c-grid/StdColumnMixin.vue'
import {filterToFn, normalizeColumnType, normalizeAction} from './c-grid/utils'

/**
 * @mixin column-mixin
 * @mixin std-column-mixin
 */
export default {
  name: 'CGridColumn',
  mixins: [ColumnMixin, StdColumnMixin],
  props: {
    columnType: {
      type: [Object, String, Function],
      default: undefined
    },
    action: {
      type: [Object, String, Function],
      default: undefined
    }
  },
  methods: {
    /**
     * @private
     */
    createColumn () {
      const columnType = normalizeColumnType(this.columnType)
      const action = normalizeAction(this.action)
      const field = this.filter ? filterToFn(this, this.field, this.filter) : this.field
      return {
        caption: this.caption || this.$el.textContent.trim(),
        field,
        columnType,
        width: this.width,
        minWidth: this.minWidth,
        maxWidth: this.maxWidth,
        action,
        style: this.columnStyle,
        sort: this.sort,
        icon: this.icon,
        message: this.message
      }
    }
  }
}

</script>

<style scoped>
.c-grid-column {
  display: none;
}
</style>
