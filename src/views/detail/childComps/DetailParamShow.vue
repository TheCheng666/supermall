<template>
  <div v-if="Object.keys(paramInfo).length !== 0">
    <table v-for="(table, index) in paramInfo.sizes" :key="index">
      <tr v-for="(tr, indey) in table" :key="indey">
        <td v-for="(td, indez) in tr" :key="indez">{{ td }}</td>
      </tr>
    </table>
    <table>
      <tr v-for="(info, index) in paramInfo.infos" :key="index">
        <td>{{ info.key }}</td>
        <td>{{ info.value }}</td>
      </tr>
    </table>
    <div v-if="paramInfo.image.length !== 0">
      <img :src="paramInfo.image">
    </div>
  </div>
</template>

<script>
export default {
  name: "DetailParamShow",
  props: {
    paramInfo: {
      type: Object,
    }
  }
}
</script>

<style scoped>

</style>