<template>
   <table class="table is-striped is-hoverable is-fullwidth is-bordered">
      <thead>
         <tr>
            <th
               v-for="column in tableConfig.columns"
               v-text="column.header"
               :key="column"
               class="table-header"
            />
         </tr>
      </thead>
      <transition name="fade" mode="out-in">
         <tbody v-if="tableConfig.content.length != 0">
            <tr
               v-for="row in tableConfig.content"
               @dblclick="selectRow(row)"
               :key="row.key"
               class="table-row is-clickable"
               @click="open(row)"
            >
               <th
                  v-for="column in tableConfig.columns"
                  v-text="row[column.key]"
                  :key="column"
               />
            </tr>
         </tbody>
      </transition>
   </table>
</template>
<script>
import { computed } from 'vue'
export default {
   props: {
      content: {
         type: Array,
         default: () => []
      },
      config: {
         type: Object,
         default: () => ({})
      },
      loading: {
         type: Boolean,
         default: false
      }
   },
   setup(props, { emit }) {
      const tableConfig = computed(() => ({
         columns: props.config.columns,
         headers: props.config.headers,
         content: props.content
      }))
      const selectRow = row => emit('select', row)
      return { tableConfig, selectRow }
   },
   methods: {
      open(row) {
         this.$emit('open', row)
      }
      // filterList = (item, search) => {
      //    const keysToFilter = ['name', 'status', 'tags']
      //    return Object.entries(item).some(
      //       ([key, value]) =>
      //          keysToFilter.includes(key) && value.toString().toLowerCase().includes(search.toLowerCase())
      //    )
      // }
   }
}
</script>
