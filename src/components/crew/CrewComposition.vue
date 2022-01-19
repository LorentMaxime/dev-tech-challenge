<template>
  <base-card>
    <!-- Member list -->
    <h2>Membres de l'équipage</h2>
    <div class="load-members">
      <base-button @click="loadArgonautes">Charger les Argonautes</base-button>
    </div>
    <p v-if="isLoading">Loading ... </p>
    <p v-else-if="!isLoading && error">{{ error }}</p>
    <p v-else-if="!isLoading && (!results || results.length === 0)">Il n'y a pas d'Argonautes enregistré(e)s pour le moment. Commencez à en ajouter !</p>
    <section class="member-list" v-else>
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
      isLoading: false,
      error: null,
    }
  },
  methods: {
    loadArgonautes() {
      const url = 'https://dev-tech-challenge-default-rtdb.europe-west1.firebasedatabase.app/surveys.json';
      this.isLoading = true;
      this.error = null;
      fetch(url)
          .then((response) => {
              if(response.ok) {
                return response.json();
              }
            }
          ).then((data) =>{
            const results = [];
            this.isLoading = false;
            for(const id in data) {
              results.push ({
                id: id,
                name: data[id].name,
              });
            }
            this.results = results;
      })
      .catch((error) =>{
        console.log(error);
        this.isLoading = false;
        this.error = 'OUPS, il semble qu\'il y ai un probleme pour recuperer les données - revenez plus tard!'
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