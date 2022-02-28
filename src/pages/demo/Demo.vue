<template>
  <div class="newPage" :style="`min-height: ${pageMinHeight}px`">
    <h1>{{$t('content')}}</h1>
    <TableSel />
  </div>
</template>

<script>
  import {mapState} from 'vuex'
  import TableSel from '@/components/tableSel/TableSel'
  export default {
    name: 'Demo',
    components: {TableSel},
    i18n: require('./i18n'),
    data() {
      return {
      }
    },
    computed: {
      ...mapState('setting', ['pageMinHeight']),
      desc() {
        return this.$t('description')
      }
    }
  }
</script>

<style scoped lang="less">
@import "index";
</style>