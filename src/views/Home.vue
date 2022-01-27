<template>
  <main class="home">
    <!---Section 1 Pais y fecha-->
    <DataTitle :text="title" :dataDate="dataDate" />
        <!---Section 2 Casos y muertes-->

    <DataBoxes :stats="stats" />
    <!---Combobox 3 paises a consultar select-->
    <CountrySelect @get-country="getCountryData" :countries="countries" />

    <!---Si selecciona el pais se habilita el button clear-->
    <button @click="clearCountryData"
    v-if="stats.Country"
    class="bg-blue-500 text-white rounded p-3 mt-10 focus:outline-none hover:bg-blue-300"
    > Clear
    </button>
  </main>
</template>

<script>

    //Importacion de componentes...

import DataTitle from '@/components/DataTitle'
import DataBoxes from '@/components/DataBoxes'
import CountrySelect from '@/components/CountrySelect'


export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect
  },
  data(){
    return{
      loading: true,
      title: 'Global',
      dataDate: '',
      status:{},
      countries: []
      
    }
  },
  // metodos de llamado de datos todos los paises
  methods:{
    async fetchCovidData(){
      const res= await fetch('https://api.covid19api.com/summary')
      const data= await res.json()
      return data
    },
      //metodo para obtener el pais
    getCountryData(country){
      this.stats=country
      this.title=country.Country
    },
// metodo para limpiar los datos y que vuelva a global
   async clearCountryData(){
     const data= await this.fetchCovidData()
     this.title='Global'
     this.stats= data.Global
    },

  },
  //llamara la fecha de hoy, los datos globales de casos y muertes
  //y su pais 
  async created(){
    const data= await this.fetchCovidData()

    this.dataDate= data.Date
    this.stats = data.Global
    this.countries= data.Countries

  }
}
</script>
