<template>
  <div class="home">
    <center><img alt="My logo" src="../assets/logo.png" height="75" width="450"></center>
    <br>
    <center><img alt="My house" v-bind:src="require(`../assets/h${x}.jpg`)" height="300" width="500"></center>
    <center>
    <div class="input-container">
    <label for="street1"> first street:</label>
    <input type="text" id="street1" v-model="userInput1" :disabled="guess1Selected" :style="{'background-color':bgcolor1}">
    <select v-model="selectedStreet1" :style="{'background-color':bgcolor1}">
      <option v-for="street in filteredStreets1" :disabled="guess1Selected" :key="street">{{ street }} </option>
    </select>
    </div>
    <div class="input-container">

    <label for="street2" >  second street:</label>
    <input type="text" id="street2" v-model="userInput2" :disabled="guess1Selected" :style="{'background-color':bgcolor2}">
    <select v-model="selectedStreet2" :style="{'background-color':bgcolor2}">
      <option v-for="street in filteredStreets2" :disabled="guess1Selected" :key="street">{{ street }}</option>
    </select>
    <button @click="setFirstGuess(selectedStreet1, selectedStreet2)" >Finalize</button>
  </div>
</center>
<br>
<br>
<center>
  <div class="input2-container">
    <label for="street3"> first street:</label>
    <input type="text" id="street3" v-model="userInput3" :disabled="!guess1Selected || guess2Selected" class="input-background-color1">
    <select v-model="selectedStreet3" class="input-background-color1">
      <option v-for="street in filteredStreets3" :disabled="!guess1Selected || guess2Selected" :key="street">{{ street }} </option>
    </select>
    </div>
    <div class="input2-container">

    <label for="street4" >  second street:</label>
    <input type="text" id="street4" v-model="userInput4" :disabled="!guess1Selected || guess2Selected" class="input-background-color2">
    <select v-model="selectedStreet4" class="input-background-color2">
      <option v-for="street in filteredStreets4" :disabled="!guess1Selected || guess2Selected" :key="street">{{ street }}</option>
    </select>
    <button @click="setSecondGuess(selectedStreet3, selectedStreet4)" >Finalize</button>
  </div>
</center>

    
    <h2>{{ finalCheck(selectedStreet1, selectedStreet2, allCorners[x]) }}</h2>
    <h2>{{ finalCheck(selectedStreet3, selectedStreet4, allCorners[x]) }}</h2>
    
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';

@Options({})
export default class Home extends Vue {
  // Lists used for all program-----------------------------------------------------------------------------------------------
  public allStreets = ['1st', 'Gavin', 'Maple', 'Olive', 'Pine', 'Redlands', 'San Mateo', "wrong", "answer"];
  public allCorners = [["madeup",  "test"] , ["wrong", "answer"], ["still", "incorrect"] ];
  public allHouse = [1,2,3,4,5,6];

  // orgininally setting players 5 guessses----------------------------------------------------------------------------------
  //first guess 
  public userInput1 = '';
  public selectedStreet1 = '';
  public userInput2 = '';
  public selectedStreet2 = '';
  public guess1Selected = false;
  //second guess
  public userInput3 = '';
  public selectedStreet3 = '';
  public userInput4 = '';
  public selectedStreet4 = '';
  public guess2Selected = false;
  
  public bgcolor1 = "white";
  public bgcolor2 = "white";

  //filtered streets for all guesses------------------------------------------------------------------------------------------
  //first guess
  public get filteredStreets1(): string[] {
    return this.allStreets.filter(street => street.toLowerCase().includes(this.userInput1.toLowerCase()));
  }
  
  public get filteredStreets2(): string[] {
    return this.allStreets.filter(street => street.toLowerCase().includes(this.userInput2.toLowerCase()));
  }

  //second guess
  public get filteredStreets3(): string[] {
    return this.allStreets.filter(street => street.toLowerCase().includes(this.userInput3.toLowerCase()));
  }
  
  public get filteredStreets4(): string[] {
    return this.allStreets.filter(street => street.toLowerCase().includes(this.userInput4.toLowerCase()));
  }

  //date functions-------------------------------------------------------------------------------------------------------------------
  getDate() {
    return new Date();
  }

  getDayOfYear(date: Date) {
    let start = new Date(date.getFullYear(), 0, 0);
    let diff = date.getTime() - start.getTime() + (start.getTimezoneOffset() - date.getTimezoneOffset()) * 60 * 1000;
    let day = Math.floor(diff / 86400000);
    return day % 4;
  }

  x = 1;//this.getDayOfYear(this.getDate());
  guess = 0;

  //selectring steets to diable after click---------------------------------------------------------------------------------------
  //first guess
  // onStreet1Selected() {
  //   this.street1Selected = true;
    
  // }
  // onStreet2Selected(){
  //   this.street2Selected = true;
  //   this.guess += 1;
  // }
  //second guess
  // onStreet3Selected() {
  //   this.street3Selected = true;
    
  // }
  // onStreet4Selected(){
  //   this.street4Selected = true;
  //   this.guess += 1;
  // }
 
  checkStreet1(k: any, j: any): boolean{
    if (j.includes(k)){
      this.bgcolor1 = "#80ff80";
      return true;
    }
    else{
      this.bgcolor1 = "#ff8080";
      return false;
    }
  }

  checkStreet2(k: any, j: any): boolean{
    if (j.includes(k)){
      this.bgcolor2 = "#80ff80";
      return true;
    }
    else{
      this.bgcolor2 = "#ff8080";
      return false;
    }
  }

  finalCheck(a: any, b: any ,c: any){
    if (a == "" || b==""){
      return "";
    }
    if (a==b){
      return "can not have same street name"
    }
    else{
      if( c.includes(a) && c.includes(b)){
        return "you got the right corner in " + this.guess + "attempts";
      }
      else{
        return "you got the wrong corner";
      }
      
    }
  }

  mounted() {
    if (localStorage.street1) {
      this.selectedStreet1 = localStorage.street1;
    }
    if (localStorage.street2) {
      this.selectedStreet2 = localStorage.street2;
    }
    if (localStorage.street3) {
      this.selectedStreet3 = localStorage.street3;
    }
    if (localStorage.street4) {
      this.selectedStreet4 = localStorage.street4;
    }

    if (localStorage.guess1Selected) {
      this.guess1Selected = localStorage.guess1Selected;
    }
    if (localStorage.guess2Selected) {
      this.guess2Selected = localStorage.guess2Selected;
    }
    if (localStorage.guess1street1 === "true") {
      this.bgcolor1 = "#80ff80";
    } else if (localStorage.guess1street1 === "false") {
      this.bgcolor1 = "#ff8080";
    } else {
      this.bgcolor1 = "white";
    }
    if (localStorage.guess1street2 === "true") {
      this.bgcolor2 = "#80ff80";
    } else if (localStorage.guess1street2 === "false") {
      this.bgcolor2 = "#ff8080";
    } else {
      this.bgcolor2 = "white";
    }
    console.log(this.bgcolor1)
    console.log(this.bgcolor2)
  }

  setFirstGuess(street1: string, street2: string) {
    localStorage.guess1street1 = this.checkStreet1(street1, this.allCorners[this.x])
    localStorage.guess1street2 = this.checkStreet2(street2, this.allCorners[this.x])
    localStorage.street1 = street1;
    localStorage.street2 = street2;
    this.guess1Selected = true;
    localStorage.guess1Selected = this.guess1Selected;
  }

  setSecondGuess(street3: string, street4: string) {
    localStorage.street3 = street3;
    localStorage.street4 = street4;
    this.guess2Selected = true;
    localStorage.guess2Selected = this.guess2Selected;
  }

  //public score = /*this.allCorners[this.x].includes(this.selectedStreet1)*/ this.checkName(this.selectedStreet1, this.allCorners[this.x],);
}
</script>

<style scoped>
.input-container{
  display: inline-block; 
}
.input2-container{
  display: inline-block;  
  
}

.input-background-color1 {
  background-color: var(--input-background-color1);
}

.input-background-color2 {
  background-color: var(--input-background-color2);
}

</style>
<!-- #80ff80 -->
<!-- #ff8080 -->