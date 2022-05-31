<template>
    <select @change="onChange" v-model="selected" class="form-select mt-10 w-full border p-3 rounded">
        <option value="0">Select Country</option>
        <option v-for="c in countries " :value="c.ID" :key="c.ID">
            {{c.Country}}
        </option>
    </select>
</template>

<script>
export default {
  name  : 'CountrySelect',
  props : ['countries'],
  data(){
      return {
          selected:  0
      }
  },
  methods : {
      onChange(){
          const country  = this.countries.find((item) => item.ID === this.selected)
          
          this.$emit('get-country', country)
      }
  }
}
</script>

<style>

</style>