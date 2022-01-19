<template>
  <base-card>
    <!-- New member form -->
    <h2>Ajouter un(e) Argonaute</h2>
    <form class="new-member-form" @submit.prevent="submitForm" :class="{invalid: invalidInput}">
      <label for="name">Nom de l&apos;Argonaute</label>
      <input id="name" name="name" type="text" size="30" placeholder="Inserez le nom de l'argonaute" v-model.trim="enteredName"/>
      <p v-if="invalidInput">Entrez un Argonaute svp</p>
      <p v-if="error">{{ error }}</p>
      <div>
        <base-button>Envoyer</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      enteredName: '',
      invalidInput: false,
      error: null,
    }
  },
  // emits: ['form-submit'],
  methods: {
    submitForm() {
      if (this.enteredName === '') {
        this.invalidInput = true;
        return;
      }
        this.invalidInput = false;

      // this.$emit ('form-submit', {
      //   argonauteName: this.enteredName
      // });

      const url = 'https://dev-tech-challenge-default-rtdb.europe-west1.firebasedatabase.app/surveys.json';
      fetch(url,{
        method:'POST',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify({
          name: this.enteredName,
        }),
      })
          .then(response => {
        if (response.ok) {
          // to do ...
        } else {
          throw new Error('Les données n\'ont pas pu etre sauvegardées - réessayer plus tard!');
        }
      })
          .catch((error) => {
        console.log(error);
        this.error = error.message;
      });

      this.enteredName = '';
    },
  },
}
</script>

<style scoped>
input {
  border-radius: 4px;
  padding: 5px;
}
.new-member-form.invalid input {
  border-color: red;
}
.new-member-form.invalid label {
  color: red;
}
.new-member-form {
  margin: 2em 0 4em 0;
  text-align: center;
}
div {
  margin-top: 1rem;
}
</style>