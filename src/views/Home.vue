<template>
  <v-form>
    <v-container>
      <v-row>
        <v-col
          cols="12"
          sm="6"
        >
          <v-text-field
            v-model="ime"
            label="First Name"
            filled
          ></v-text-field>
          <v-btn color="success" class="mb-5" @click="mounted">Submit</v-btn>
        </v-col>
      {{prvo}}
      {{ime}}
      </v-row>
    </v-container>
  </v-form>
</template>

<script>


export default {
  name: 'Home',
  data: function () {
    return {
      prvo: [],
      ime: ""
    };
  },
  async mounted() {
    let rezultat = await fetch(
      'https://api.nationalize.io?name=' + this.ime
    );
    let podaci = await rezultat.json();


    this.prvo = podaci;
  },
}
</script>
