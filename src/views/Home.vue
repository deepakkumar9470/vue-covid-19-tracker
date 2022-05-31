<template>
  <main  v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate"/>
    <DataBoxes :stats="stats"/>
    <CountrySelect :countries="countries" @get-country="getCountry"/>
    <button 
    @click="clearCountryData"
    v-if="stats.Country"
    class="bg-blue-500 hover:bg-blue-700 text-white font-bold mt-10 py-2 px-4 rounded">
      Reset
  </button>
  </main>

  <main class="flex flex-col align-center justify-center" v-else>
       <div class="text-gray-500 text-3xl mt-1 mb-6">
         Fetching Data...
       </div> 
       <img :src="loadingImage" class="w-24 mx-auto" alt="loadingimage">
  </main>
</template>


<script>
import Header from '@/components/Header.vue'
import DataTitle from '@/components/DataTitle.vue'
import DataBoxes from '@/components/DataBoxes.vue'
import CountrySelect from '@/components/CountrySelect.vue'

export default {
  name: 'HomeView',
  components : {
    Header,
    DataTitle,
    DataBoxes,
    CountrySelect
},
  data () {
    return {
      loading: true,
      title : 'Global',
      dataDate : '',
      stats : {},
      countries : [],
      loadingImage : require('../assets/hourglass.gif')
    }
  },
  methods : {
   async fetchCovid () {
     const res = await fetch('https://api.covid19api.com/summary')
     const data = await res.json()
     return data
   },
   getCountry(country){
     this.stats = country
     this.title = country.Country
   },
  async  clearCountryData(){
     this.loading = true
     const data = await this.fetchCovid()
     this.title = 'Global'
     this.stats = data.Global
     this.loading = false
  }
  },

 async created (){
     const data = await this.fetchCovid()
     console.log(data)
     this.dataDate = data.Date
     this.stats = data.Global
     this.countries = data.Countries
     this.loading = false

  }
}
</script>
