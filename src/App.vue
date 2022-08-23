<template>
  <v-app>
    <v-card v-if="!etat" class="mx-auto my-16" width="800" height="400">
      <v-row>
        <v-col>
          <v-img class="mx-auto my-16 ml-10"
            height="220" width="220" src="https://via.placeholder.com/750x600">
          </v-img>
        </v-col>
          <v-col class="mx-auto my-16 ml-9">
            <v-chip label color="blue" text-color="white">{{compteur +1}} - 5</v-chip>
            <v-card-subtitle>{{variable[compteur].label}}</v-card-subtitle>
            <v-btn class="mb-2" width="350" color="blue" @click="validate(0)" :disabled="disable">{{variable[compteur].answers[0].label}}</v-btn><br>
            <v-btn class="mb-2" width="350" color="blue" @click="validate(1)" :disabled="disable">{{variable[compteur].answers[1].label}}</v-btn><br>
            <v-btn class="mb-2" width="350" color="blue" @click="validate(2)" :disabled="disable">{{variable[compteur].answers[2].label}}</v-btn><br>
            <v-btn class="mb-2" width="350" color="blue" @click="validate(3)" :disabled="disable">{{variable[compteur].answers[3].label}}</v-btn><br>
            <v-btn class="mb-2" color="green" @click="next()">Next</v-btn>
          </v-col>
          <v-col class="mx-auto my-16 ml-10">
            00:{{timerCount}}
          </v-col>
      </v-row>
    </v-card>
    <v-card v-if="etat" class="mx-auto my-16" width="800" height="400">
      <v-card-subtitle>
        <div style="text-align: center;">
          <p class="mb-6">{{this.result}} / 5</p>
          <v-btn class="mb-6" color="green">Confirm your test</v-btn><br>
          <v-btn class="mb-6" color="green" @click="reload()">Restart Test</v-btn>
        </div>
      </v-card-subtitle>
    </v-card>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  components: {
  },

  data: () => ({
    timerCount: 59,
    disable: false,
    etat: false,
    result: 0,
    compteur: 0,
    compteurResponse: 10,
    variable: [
      {"id":1,"answers":[{"id":11,"label":"Rabat","correct":true},{"id":12,"label":"Casablanca","correct":false},{"id":13,"label":"Agadir","correct":false},{"id":14,"label":"Tanger","correct":false}],"image":"https://via.placeholder.com/750x600","label":"Capitale du maroc ?","time":60},
      {"id":2,"answers":[{"id":21,"label":"Espagne","correct":true},{"id":22,"label":"italie","correct":false},{"id":23,"label":"france","correct":false},{"id":24,"label":"portugal","correct":false}],"image":"https://via.placeholder.com/750x600","label":"Dans quel pays peut-on trouver la Catalogne, l'Andalousie et la Castille ?","time":30},
      {"id":3,"answers":[{"id":31,"label":"Vercingétorix","correct":false},{"id":32,"label":"César","correct":true},{"id":33,"label":"Attila","correct":false},{"id":34,"label":"Augustus","correct":false}],"image":"https://via.placeholder.com/750x600","label":"Qui a dit : « Le sort en est jeté » (Alea jacta est) ?","time":60},
      {"id":4,"answers":[{"id":41,"label":"L'Argentine","correct":false},{"id":42,"label":"L'Allemagne","correct":true},{"id":43,"label":"L'Italie","correct":false},{"id":44,"label":"Le Brésil","correct":false}],"image":"https://via.placeholder.com/750x600","label":"Quel pays a remporté la coupe du monde de football en 2014 ?","time":60},
      {"id":5,"answers":[{"id":51,"label":"Léonardo DiCaprio","correct":false},{"id":52,"label":"Brad Pitt","correct":false},{"id":53,"label":"Matthew MacConaughey","correct":true},{"id":54,"label":"Tom Cruise","correct":false}],"image":"https://via.placeholder.com/750x600","label":"Quel acteur américain incarne le héros du film de Christopher Nolan de 2014 « Interstellar » ?","time":60}
    ]
  }),

  methods:{
    validate(__param){
      if(this.variable[this.compteur].answers[__param].correct == true) 
      {
        this.result = this.result + 1;
      }
      this.disable = true;
    },
    next(){
      this.compteur = this.compteur + 1; 
      if(this.compteur >= 5) this.etat = true;
      this.disable = false;
    },
    reload(){
      window.location.reload();
    },
  },
  watch: {
    timerCount: {
        handler(value) {
            if (value > 0) {
                setTimeout(() => {
                    this.timerCount--;
                }, 1000);
            }
            if(value == 0) this.etat = true;
        },
        immediate: true 
    }
}
};
</script>
