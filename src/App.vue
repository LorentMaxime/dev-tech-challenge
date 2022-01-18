<template>
  <!-- Header section -->
  <the-header></the-header>

  <!-- Main section -->
  <main>
    <adding-member></adding-member>
    <crew-composition></crew-composition>
  </main>

  <!-- Footer section -->
  <the-footer></the-footer>
</template>

<script>
import TheHeader from '@/components/layouts/TheHeader';
import TheFooter from '@/components/layouts/TheFooter';
import AddingMember from '@/components/crew/AddingMember';
import CrewComposition from '@/components/crew/CrewComposition';

export default {
    components: {
    TheHeader,
    TheFooter,
    AddingMember,
    CrewComposition,
  },
  // data() {
  //   return {
  //     savedArgonautes: [],
  //   }
  // },
  // methods: {
  //   storeArgonaute(value) {
  //     const formResult = {
  //       name: value.argonauteName,
  //       id: new Date().toISOString(),
  //     }
  //     this.savedArgonautes.push(formResult)
  //     console.log(this.savedArgonautes);
  //   },
  // },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

body {
  margin: 0;
  font-family: 'Roboto', sans-serif;
}

main {
  max-width: 960px;
  margin: 0 auto;
}

h1, h2 {
  text-align: center;
}

label {
  display: block;
  margin-bottom: 0.5em;
}

</style>
