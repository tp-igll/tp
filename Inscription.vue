<template>
<div class="Inscription">
   <v-card class="my-5">
        <v-card-title class="blue darken-3" style="color: white;font-family: sans-serif;">
          Inscrire étudiant
        </v-card-title>
        <v-container grid-list-sm>
          <v-layout
            row
            wrap
          >
            <v-flex xs6>
              <v-text-field
                
                placeholder="Nom"
                prepend-icon="mdi-account"
              ></v-text-field>
            </v-flex>
            <v-flex xs6>
              <v-text-field
                placeholder="Prénom"
              ></v-text-field>
            </v-flex>

            <v-flex xs12>
              <v-text-field
                prepend-icon="mdi-email"
                placeholder="Email"
              ></v-text-field>
            </v-flex>
            
             <v-flex xs12>
  
        <v-menu
          ref="menu1"
          v-model="menu1"
          :close-on-content-click="false"
          transition="scale-transition"
          offset-y
          full-width
          max-width="290px"
          min-width="290px"
        >
          <template v-slot:activator="{ on }">
            <v-text-field
              v-model="dateFormatted"
              label="Date de naissance"
              persistent-hint
              prepend-icon="mdi-calendar-range"
              @blur="date = parseDate(dateFormatted)"
              v-on="on"
            ></v-text-field>
          </template>
          <v-date-picker v-model="date" no-title @input="menu1 = false"></v-date-picker>
        </v-menu>
      </v-flex>
            <v-flex xs12>
              <v-text-field
                prepend-icon="mdi-home"
                placeholder="Adresse"

              ></v-text-field>
            </v-flex>
            <v-flex xs12>
              <v-text-field
                type="tel"
                prepend-icon="mdi-phone"
                placeholder="Téléphone"
              ></v-text-field>
            </v-flex>
            <v-flex xs12>
              <v-text-field
                prepend-icon="mdi-adjust"
                placeholder="Matricule"
              ></v-text-field>
            </v-flex>
          </v-layout>
        </v-container>
        <v-card-actions>
          <v-spacer></v-spacer>
            <v-btn class="ma-2" color="primary" dark>Inscrire
        <v-icon dark right>mdi-checkbox-marked-circle</v-icon>
            </v-btn>
        </v-card-actions>
      </v-card>
</div>

</template>

<script>
  export default {
    data: vm => ({
      date: new Date().toISOString().substr(0, 10),
      dateFormatted: vm.formatDate(new Date().toISOString().substr(0, 10)),
      menu1: false,
      menu2: false,
    }),

    computed: {
      computedDateFormatted () {
        return this.formatDate(this.date)
      },
    },

    watch: {
      date () {
        this.dateFormatted = this.formatDate(this.date)
      },
    },

    methods: {
      formatDate (date) {
        if (!date) return null

        const [year, month, day] = date.split('-')
        return `${month}/${day}/${year}`
      },
      parseDate (date) {
        if (!date) return null

        const [month, day, year] = date.split('/')
        return `${year}-${month.padStart(2, '0')}-${day.padStart(2, '0')}`
      },
    },
  }
</script>