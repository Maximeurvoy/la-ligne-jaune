<template>
  <div>
  <p>My position latitude {{latPosition}} longitude {{lonPosition}}<p/>
  {{wcPosition}}
  <ul>
    <li v-for="item in info" v-bind:key="item.index">
     toilette : Latitude {{ item[0] }} longitude {{ item[1] }}
    </li>
  </ul>
  {{info}}
  <p> test map bordel d'axios !</p>
  </div>
</template>
<script>
const axios = require('axios')
/* eslint-disable */
export default {

  data () {
    return {
      wcPosition: null,
      latPosition: 'future latitude',
      lonPosition: 'future longitude',
      items: [
        {message: 'foo'},
        {message: 'test'}
      ]
    }
  },
  mounted () {
    axios.get('https://data.nantesmetropole.fr/api/records/1.0/search/?dataset=244400404_toilettes-publiques-nantes-metropole&facet=commune&facet=pole&facet=type&facet=automatique&facet=acces_pmr')
      .then(response => {
        const toilettes = response.data.records
        console.log(toilettes)
        const wherePiss = toilettes.map((toilette, index) =>
          toilette.fields.location)
        console.log(wherePiss)
        this.wcPosition = wherePiss
      })
    console.log('fhjdhj')

    navigator.geolocation.getCurrentPosition(position => {
      this.latPosition = position.coords.latitude
      this.lonPosition = position.coords.longitude
    })
  }
}
</script>

  <style>
  </style>
