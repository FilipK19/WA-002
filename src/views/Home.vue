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
            label="Upisi ime"
            filled
          ></v-text-field>
          <v-btn color="success" class="mb-5" @click="getData">Prikazi podatke</v-btn>
        </v-col>
      </v-row>
      <div>
            <v-data-table
            :headers="headers"
            :items="tableData"
            :items-per-page="3"
            class="elevation-1"
        ></v-data-table>
        </div>
    </v-container>
  </v-form>
</template>

<script>


export default {
  name: 'Home',
  data: function () {
    return {
      detaljime: [],
      detaljime2: [],
      detaljime3: [],
      tableData: [],
      newData: [],

      headers: [
      {
        text: "Ime",
        align: "start",
        sortable: false,
        value: "name",
      },
      { text: "Država", value: "country" },
      { text: "Vjerojatnost drzave", value: "countryProb" },
      { text: "Dob", value: "age" },
      { text: "Spol", value: "gender" },
      { text: "Vjerojatnost spola", value: "genderProb" },
    ],
    };
  },
  
  methods: {
  async getData() {
    let rezultat = await fetch(
      'https://api.nationalize.io?name=' + this.ime);
    let podaci = await rezultat.json();
    this.detaljime = podaci;

    let rezultat2 = await fetch(
      'https://api.agify.io?name=' + this.ime);
    let podaci2 = await rezultat2.json();
    this.detaljime2 = podaci2;

    let rezultat3 = await fetch(
      'https://api.genderize.io?name=' + this.ime);
    let podaci3 = await rezultat3.json();
    this.detaljime3 = podaci3;
  

    let array1 = [];
      this.nameData = [this.detaljime2, this.detaljime3, this.detaljime];
      this.nameData = this.nameData[2].country.forEach((country) =>
        array1.push([this.nameData[0], this.nameData[1], country])
      );
      let array2 = [];
      array1.forEach((array) =>
        array2.push({
          name: array[0].name,
          age: array[0].age,
          country: array[2].country_id,
          countryProb: array[2].probability,
          gender: array[1].gender,
          genderProb: array[1].probability,
          
        })
      );
      this.tableData = array2;
  }
  }
}
</script>
