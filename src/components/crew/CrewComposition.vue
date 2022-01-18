<template>
  <base-card>
    <!-- Member list -->
    <h2>Membres de l'équipage</h2>
    <div class="load-members">
      <base-button @click="loadArgonautes">Charger les Argonautes</base-button>
    </div>
    <section class="member-list">
      <div class="member-item">
        <ul>
          <form-result v-for="result in results"
                       :key="result.id"
                       :name="result.name"></form-result>
        </ul>
      </div>
    </section>
  </base-card>
</template>

<script>
import FormResult from './FormResult';

export default {
  // props: ['name'],
  components: {
    FormResult,
  },
  data() {
    return {
      results: [],
    }
  },
  methods: {
    loadArgonautes() {
      // const url = 'https://dev-tech-challenge-default-rtdb.europe-west1.firebasedatabase.app/surveys.json';
      fetch('https://dev-tech-challenge-default-rtdb.europe-west1.firebasedatabase.app/surveys.json')
          .then((response) => {
              if(response.ok) {
                return response.json();
              }
            }
          ).then((data) =>{
            const results = [];
            for(const id in data) {
              results.push ({
                id: id,
                name: data[id].name,
              });
            }
            this.results = results;
      });
    },
  },
  mounted() {
    this.loadArgonautes();
  }
}
</script>

<style scoped>
 .load-members {
   margin-top: 0;
   text-align:center;
 }
 .member-item {
   padding: 1rem 0;
 }
 ul {
   list-style: none;
   margin: 0;
   padding: 0;
   display: grid;
   grid-template-columns: repeat(3, 1fr);
   justify-items: center;
 }
</style>