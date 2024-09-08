<template>
    <v-container>
      <v-row>
        <v-col cols="12">
          <h1 class="text-center">Kontaktirajte Nas</h1>
          <v-divider class="my-4"></v-divider>
          <v-card class="pa-4">
            <v-card-title>Kontakt Informacije</v-card-title>
            <v-card-subtitle>
              Ako imate bilo kakvih pitanja ili komentara, slobodno nas kontaktirajte na dolje navedene informacije:
            </v-card-subtitle>
            <v-card-text>
              <v-list>
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>mdi-email</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title>Email: info@example.com</v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>mdi-phone</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title>Telefon: +123 456 789</v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>mdi-map-marker</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <v-list-item-title>Adresa: 1234 Ulica, Grad, Zemlja</v-list-item-title>
                  </v-list-item-content>
                </v-list-item>
              </v-list>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
  <script>
  export default {
    name: "ContactView",
  };
  </script>
  
  <style scoped>
  .text-center {
    text-align: center;
  }
  </style>
  