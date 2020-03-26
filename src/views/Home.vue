<template>
  <div class="home">    
    <Plist :todo="plantel" title="Plantel" direction="right" />
    <Plist :todo="plantilla" title="Plantilla" direction="left" />
  </div>
</template>

<script>
// @ is an alias to /src
//import Todo from '@/components/EjemploTodoList.vue'
import Plist from '@/components/PlayersList.vue'

/*
<b-container algin-v="center">
      <b-row>
        <b-col>1 of 3</b-col>
        <b-col>2 of 3</b-col>
        <b-col>3 of 3</b-col>
      </b-row>
    </b-container>  
*/
export default {
  name: 'Home',
  data: function(){
    return {
          plantilla: [
              { id:1, label: "G. Viscarra", pos: "POR", posnum: 1, age: 27, done: false },
              { id:4, label: "M. Riquelme", pos: "ATA", posnum: 4, age: 32, done: false },
              { id:2, label: "A. Jusino", pos: "DEF", posnum: 2, age: 26, done: false },
              { id:3, label: "C. Machado", pos: "MED", posnum: 3, age: 30, done: false },              
              { id:7, label: "V. Ábrego", pos: "ATA", posnum: 4, age: 22, done: false },
              { id:5, label: "R. Domínguez", pos: "DEF", posnum: 2, age: 22, done: false },
              { id:6, label: "J. Rojas", pos: "POR", posnum: 1, age: 24, done: false },
          ],
          plantel: [
              
              { id:8, label: "V. Castellón", pos: "ATA", posnum: 4, age: 29, done: false },
              { id:9, label: "L. Gutiérrez", pos: "DEF", posnum: 2, age: 33, done: false },
              { id:10, label: "P. Azogue", pos: "MED", posnum: 3, age: 25, done: false },              
              { id:11, label: "J. Pereyra", pos: "ATA", posnum: 4, age: 30, done: false },
              { id:12, label: "C. Paredes", pos: "DEF", posnum: 2, age: 26, done: false },
              { id:13, label: "W. Rojas", pos: "POR", posnum: 1, age: 24, done: false },
          ]
    }
  },
  methods: {
    toPlantillaList: function(item){
      this.plantel = this.plantel.filter(function( obj ) {
       return obj.id !== item.id;
      });
      this.plantilla.push(item);
    },
    toPlantelList: function(item){
      this.plantilla = this.plantilla.filter(function( obj ) {
       return obj.id !== item.id;
      });
      this.plantel.push(item);
    }
  }
  ,
  components: {
    Plist,
    // Todo
  }
}
</script>
