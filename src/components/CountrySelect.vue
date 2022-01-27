<template>
<!--El select donde selecciona el pais a consultar-->
    <select @change="onChange()"
     v-model="selected"
      class="form-select mt-10 block w-full border p-3 rounded"
      >
        <option value="0">Select Country</option>
        <!---<div v-for="(item, index) in items" :key="item.id">
    {{index}}. {{item.name}}
</div>
Implementar el siguiente algoritmo--->
                <option v-for="country in countries" :value="country.ID">
                    {{country.Country}}
                </option>
                <!--Fin de algoritmo de obtencion de paises de la api--->
    </select>
</template>

<script>
export default {
    name: 'CountrySelect',
    props: ['countries'],
    data(){
        return{
            selected: 0,
        }
    },
    methods: {
        onChange(){
            const country = this.countries.find((item)=> item.ID === this.selected)
            console.log(country)
            this.$emit('get-country',country)
        },
    },
}
</script>