<template>
  <tfoot v-show="data.length">
    <tr class="-summary-row" v-for="(cs, idx) in customSummary">
      <td v-if="shouldRenderSelection"></td>
      <template v-for="(col, idx) in columns">
        <!-- display the available fields only -->
        <td v-if="typeof cs[col.field] !== 'undefined'" :class="cs[col.field].tdClass" :style="cs[col.field].tdStyle">
          <!-- <td> component (tdComp) -->
          <component
            v-if="cs[col.field].tdComp"
            :is="forDynCompIs(cs[col.field].tdComp)"
            :row="cs"
            :field="col.field"
            :value="cs[col.field].value"
            v-bind="$props">
          </component>
          <template v-else>
            {{ cs[col.field].value }}
          </template>
        </td>
        <td v-else></td>
      </template>
    </tr>
  </tfoot>
</template>
<script>
import props from '../_mixins/props'
import shouldRenderSelection from '../_mixins/shouldRenderSelection'

export default {
  name: 'TableCustomFooter',
  mixins: [props, shouldRenderSelection]
}
</script>
<style>
.-summary-row {
  font-weight: bold;
  background-color: #eee !important;
}
</style>
