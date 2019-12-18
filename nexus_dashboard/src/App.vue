<template>
  <div id="app">
<!--     <Header></Header>-->
<!--    <CustomChart></CustomChart>-->
<!--    <VerticalChart></VerticalChart>-->
<!--    <PieChart></PieChart>-->
<!--    <ClickableList></ClickableList>-->
<!--    <Form></Form>-->
    <div>
      <div class="floating-form">
        <p class="title">Paramètres</p>
        <form action="#">
          <table>
            <tr>
              <td><input type="text" v-model="x0" placeholder="Germe (x0)"></td>
            </tr>
            <tr>
              <td><input type="text" v-model="a" placeholder="a"></td>
            </tr>
            <tr>
              <td><input type="text" v-model="c" placeholder="c"></td>
            </tr>
            <tr>
              <td><input type="text" v-model="m" placeholder="m"></td>
            </tr>
          </table>
          <a href="" class="round-btn" @click.prevent="simulation()">submit</a>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import FloatingBox from './components/FloatingBox';
import ClickableList from './components/ClickableList';
import CustomChart from './components/CustomChart';
import VerticalChart from './components/VerticalChart';
import PieChart from './components/PieChart';
import Form from './components/Form';
import Header from './components/Header';
import RechopForm from './components/RechopForm';


export default {
  name: 'App',
  components: {
    FloatingBox,
    ClickableList,
    CustomChart,
    VerticalChart,
    PieChart,
    Form,
    Header,
    RechopForm,
  },
  data() {
    return {
      NB_PLACE_PRIO: 5,
      COUT_CHGT_FILE: 50,
      COUT_CLIENT_PRIO: 40,
      COUT_CLIENT_ORDINAIRE: 25,
      COUT_STATION_OCC: 35,
      COUT_STATION_INOCC: 20,
      coutMin: 999999999999999999,
      tempsSimulation: 600,
      nbStation: 4,
      NB_STATION_MAX: 24,
      stations: [],
      stationsOptimal: 0,
      filePrio: 0,
      x0: 356,
      xn: 0,
      a: 63,
      c: 57,
      m: 32767,
      file: 0,
      sorties: [],
      totArrivee: 0,
      iteration: {
        arrivees : [],
      },
  };
  },
  methods: {
    genererNbAleatoire() {
      console.log("--------------  Generer aleatoire --------------");
      this.xn = ((this.a * this.xn) + this.c) % this.m;
      return this.xn / this.m;
    },

    generationNbArrivees() {
      console.log("--------------  Générer Arrivées --------------");
      let un = this.genererNbAleatoire();

      if (un < 0.165) return 0;
      if (un < 0.463) return 1;
      if (un < 0.731) return 2;
      if (un < 0.891) return 3;
      if (un < 0.964) return 4;
      if (un < 0.99) return 5;
      if (un < 0.997) return 6;
      if (un < 0.999) return 7;
      return 8;
    },

    generationDureeService() {
      console.log("--------------  GenererDureeService --------------");
      let un = this.genererNbAleatoire();

      if (un < 0.3050847458) return 1;
      if (un < 0.6610169492) return 2;
      if (un < 0.9152542373) return 3;
      if (un < 0.9661016949) return 4;
      if (un < 0.9830508475) return 5;
      return 6;
    },

    placementEnStationNormale() {
      console.log("--------------  Placement en file normale --------------");
      let i = 1;

      while (i < this.stations.length && (this.filePrio + this.file ) > 0) {
        let dureeService = this.generationDureeService();
        console.log("CAS NORMAL DureeService :"+dureeService);
        this.stations[i].dureeService = dureeService;
        // console.log(JSON.stringify(this.stations[i]));

        if (this.file === 0) {
          this.filePrio--;
          this.stations[i].possedePrio = true;
          // console.log("added prio statnormal "+JSON.stringify(this.stations));
        } else {
          this.file--;
          // console.log("added id statnormal "+JSON.stringify(this.stations));
        }
        i++;
      }
    },

    traitement() {
      console.log("--------------  Traitement --------------");
      let coutMinute = 0;
      if (this.stations[0].dureeService === 0 && this.filePrio > 0) {
        let dureeService = this.generationDureeService();
        console.log("(CAS PRIO) Duree service :"+dureeService);
        this.stations[0].dureeService = dureeService;
        this.stations[0].possedePrio = true;
        this.filePrio--;
        // console.log("added id statprio "+JSON.stringify(this.stations));
      }

      this.placementEnStationNormale();
      console.log("--------------  Fin Placement en stations --------------");
      console.log(JSON.stringify(this.stations));
      this.iteration.stationsAvantTrt = this.clone(this.stations);
      let i = 0;
      while (i < this.stations.length) {
        console.log("--------------  Traitement des stations --------------");
        if (this.stations[i].dureeService === 0) {
          coutMinute += this.COUT_STATION_INOCC/60;
        } else {
          coutMinute += this.COUT_STATION_OCC/60;
          if (i === 0 || this.stations[i].possedePrio) {
            coutMinute += this.COUT_CLIENT_PRIO/60;
          } else {
            coutMinute += this.COUT_CLIENT_ORDINAIRE/60;
          }
          this.stations[i].dureeService--;
          if (this.stations[i].dureeService === 0 && this.stations[i].possedePrio) {
            this.stations[i].possedePrio = false;
          }
        }
        i++;
      }
      coutMinute += (this.file * (this.COUT_CLIENT_ORDINAIRE/60)) + (this.filePrio *(this.COUT_CLIENT_PRIO/60));
      // console.log(coutMinute);
      return coutMinute;
    },
    initStations() {
      console.log("--------------  InitStations --------------");
      let i = 0;
      while (i < this.nbStation) {
        this.stations.push({
          dureeService: 0,
          possedePrio: false,
        });
        i++;
      }
      console.log(JSON.stringify(this.stations));
    },
    clone(obj) {
      // Handle the 3 simple types, and null or undefined
      if (null == obj || "object" != typeof obj) return obj;

      // Handle Date
      if (obj instanceof Date) {
        var copy = new Date();
        copy.setTime(obj.getTime());
        return copy;
      }

      // Handle Array
      if (obj instanceof Array) {
        var copy = [];
        for (var i = 0, len = obj.length; i < len; i++) {
          copy[i] = this.clone(obj[i]);
        }
        return copy;
      }

      // Handle Object
      if (obj instanceof Object) {
        var copy = {};
        for (var attr in obj) {
          if (obj.hasOwnProperty(attr)) copy[attr] = this.clone(obj[attr]);
        }
        return copy;
      }
    },
    simulation() {
      console.log("--------------  Début programme --------------");
      this.a = this.a - "";
      this.c = this.c - "";
      this.m = this.m - "";
      this.x0 = this.x0 - "";

      while (this.nbStation < this.NB_STATION_MAX) {
        console.log("--------------  BoucleStation : nbStation ="+this.nbStation+" --------------");
        this.xn = this.x0;
        let couts = 0;
        this.file = 0;
        this.filePrio = 0;
        this.stations = [];
        this.initStations();
        this.totArrivee = 0;

        this.iteration = {
          arrivees : [],
        };

        let t = 1;

        while (t <= this.tempsSimulation) {
          console.log("--------------  Simulation avec temps ="+t+" --------------");
          let nbArrivees = this.generationNbArrivees();
          this.iteration.arrivee = nbArrivees+" arrivées cette itération";
          console.log("NbArrivees :"+nbArrivees);
          this.totArrivee += nbArrivees;
          this.iteration.stationsAuDebut = this.clone(this.stations);

          while (nbArrivees > 0) {
            console.log("--------------  Boucle sur nbArrivee --------------");
            console.log("--------------  GenererPrio --------------");
            let priorite = this.genererNbAleatoire();
            let arrivee = {
              prioritaire: false,
            };

            if (priorite < 0.3 && this.filePrio < this.NB_PLACE_PRIO) {
              arrivee.prioritaire = true;
              this.filePrio++;
              console.log("Client est prio en file prio");
            } else {
              if (priorite < 0.3) {
                couts += this.COUT_CHGT_FILE;
              } else {
                arrivee.prioritaire = false;
              }
              console.log("Client en file normale");
              this.file++;
            }
            this.iteration.arrivees.push(arrivee);
            nbArrivees--;
          }

          this.iteration.fileNormale = "Avant traitement file normale = "+this.file+"";
          this.iteration.filePrio = "Avant traitement file prio = "+this.filePrio+"";
          let coutMinute = this.traitement();
          this.iteration.fileNormaleApresTrt = "Apres traitement file normale = "+this.file+"";
          this.iteration.filePrioApresTrt = "Apres traitement file prio = "+this.filePrio+"";
          console.log("--------------  Fin traitement --------------");
          console.log(JSON.stringify(this.stations));
          console.log("Etat file normale :"+this.file);
          console.log("Etat file Prio :"+this.filePrio);
          // console.log("coutMinute "+coutMinute);
          // console.log("stations finales "+JSON.stringify(this.stations));

          couts += coutMinute;
          this.iteration.stationsEnFin = this.clone(this.stations);
          if (t <= 20) {
            this.sorties.push(this.clone(this.iteration));
          }
          // console.log(JSON.stringify(this.stations));
          t++;
        }

        console.log("Couts avec "+this.nbStation+" stations : "+couts);
        if (couts < this.coutMin) {
          this.coutMin = couts;
          this.stationsOptimal = this.nbStation;
          // console.log("xxxxxxxxxxxxxxxxxxxxx "+this.stationsOptimal);
        }
        // console.log("couts "+couts);
        // console.log("coutMin "+this.coutMin);
        // console.log(this.nbStation+"-"+this.totArrivee);
        this.nbStation++;
      }
    }
  },
};
</script>

<style src = "./components/main.css">
</style>
