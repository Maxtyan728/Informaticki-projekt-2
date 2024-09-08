<template>
  <v-dialog v-model="modal" max-width="500px">
    <v-card>
      <v-card-title class="headline">Dodaj novu recenziju</v-card-title>
      <v-card-text>
        <v-form ref="form" v-model="formIsValid">
          <v-text-field
            v-model="reviewTitle"
            label="Naslov"
            required
          ></v-text-field>
          <v-text-field
            v-model="author"
            label="Autor"
            required
          ></v-text-field>
          <v-textarea
            v-model="reviewContent"
            label="Sadržaj recenzije"
            required
          ></v-textarea>
        </v-form>
        <v-alert
          type="success"
          v-model="successAlert"
          class="mt-4"
        >
          Uspješno ste dodali svoju recenziju!
        </v-alert>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn @click="submitReview" color="primary">Dodaj</v-btn>
        <v-btn @click="modal = false">Odustani</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data() {
    return {
      modal: false,
      reviewTitle: '',
      reviewContent: '',
      successAlert: false,
      formIsValid: false,
    };
  },
  methods: {
    submitReview() {
      this.successAlert = true;
      setTimeout(() => {
        this.successAlert = false;
        this.modal = false;
      }, 1000); 
    },
  },
};
</script>
