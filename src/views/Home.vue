<template>
  <div class="home">
  <v-form>
    <v-container>
      <v-row>
        <v-col
          cols="12"
          sm="6"
        >
          <v-text-field
            v-model="first"
            label="First Name"
            filled
          ></v-text-field>
        </v-col>

      </v-row>
    </v-container>
  </v-form>
  </div>
</template>

<script>


export default {
  name: 'Home',
  components: {
    
  }
}
</script>
