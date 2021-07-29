<template>
  <div class="home">
    <br>
    <p style="font-family:Roboto; font-size:18pt">SIT Subject Reservation Web - on vercel</p>
    <br>
    <v-row justify="center" align="top" no-gutters style="height: 150px;">
      <v-col v-for="n in 3" :key="n" cols="3">
        <subject/>
      </v-col>
    </v-row>
  </div>
</template>


<script>
  import Subject from '../components/Subject'
  export default {
    name: 'Home',
    components: {
      Subject,
    },
    data: () => ({
      alignments: [
        'start',
        'center',
        'end',
      ],
    })
  }
</script>
