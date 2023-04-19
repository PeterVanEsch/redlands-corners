<template>
  <div class="home">
    <center>
      <img alt="My logo" src="../assets/logo.png" height="75" width="480" >
    </center>
    <br>
    <center>
      <img alt="My house" v-bind:src="require(`../assets/h${x}.jpg`)" height="300" width="500" style="border: 6px solid #000000; padding: 10px; margin: 5px;">
    </center>
    <center :class="{shake: disabled1 || disabled2}">
      <div class="input-container">
        <input class="tt" :class="{redoutline: disabled1}" type="search" @change="disabled1=false" placeholder="First street" list="data" v-model="selectedStreet1" :disabled="guess1Selected" :style="{backgroundColor: bgcolor1}"/>
        <datalist id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
      </div>
      <label style="font-size: 30px;"> + </label>
      <div class="input-container">
        <input  class="tt" :class="{redoutline: disabled2}" type="search" @change="disabled2=false" placeholder="Second street" list="data" v-model="selectedStreet2" :disabled="guess1Selected" :style="{'background-color':bgcolor2}"/>
        <datalist id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
        <button class="buttonG1" @click="setFirstGuess(selectedStreet1, selectedStreet2)" >Guess</button>
      </div>
    </center>
    <br>
    <center>
      <div class="input-container">
        <input  class="tt" type="search" placeholder="First street" list="data" v-model="selectedStreet3" :disabled="guess2Selected || !guess1Selected" :style="{'background-color':bgcolor3}"/>
        <datalist id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
      </div>
      <label> and </label>
      <div class="input-container">
        <input class="tt" type="search" placeholder="Second street" list="data" v-model="selectedStreet4" :disabled="guess2Selected || !guess1Selected" :style="{'background-color':bgcolor4}"/>
        <datalist  id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
        <button class="buttonG1" @click="setSecondGuess(selectedStreet3, selectedStreet4)" >Guess</button>
      </div>
    </center>
    <br>
    <center>
      <div class="input-container">
        <input  class="tt" type="search" placeholder="First street" list="data" v-model="selectedStreet5" :disabled="guess3Selected || !guess2Selected" :style="{'background-color':bgcolor5}"/>
        <datalist id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
      </div>
      <label> and </label>
      <div class="input-container">
        <input class="tt" type="search" placeholder="Second street" list="data" v-model="selectedStreet6" :disabled="guess3Selected || !guess2Selected" :style="{'background-color':bgcolor6}"/>
        <datalist  id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
        <button class="buttonG1" @click="setThirdGuess(selectedStreet5, selectedStreet6)" >Guess</button>
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
  public allStreets = ['1st', 'Gavin', 'Maple', 'Olive', 'Pine', 'Redlands', 'San Mateo', "wrong", "answer", "still", "incorrect", "what", "the", "ryan", "is", "so", "dumb", ];
  public allCorners = [["madeup",  "test"] , ["wrong", "answer"], ["still", "incorrect"] ];
  public allHouse = [1,2,3,4,5,6];
  // orgininally setting players 5 guessses----------------------------------------------------------------------------------
  //first guess 
  public selectedStreet1 = '';
  public selectedStreet2 = '';
  public guess1Selected = false;
  public bgcolor1 = "white";
  public bgcolor2 = "white";
  //second guess
  public selectedStreet3 = '';
  public selectedStreet4 = '';
  public guess2Selected = false;
  public bgcolor3 = "white";
  public bgcolor4 = "white";
  //third guess
  public selectedStreet5 = '';
  public selectedStreet6 = '';
  public guess3Selected = false;
  public bgcolor5 = "white";
  public bgcolor6 = "white";

  public disabled1 = false;
  public disabled2 = false;
  
  //date functions-------------------------------------------------------------------------------------------------------------------
  getDate() {
    return new Date();
  }
  getDayOfYear(date: Date) {
    let start = new Date(date.getFullYear(), 0, 0);
    let diff = date.getTime() - start.getTime() + (start.getTimezoneOffset() - date.getTimezoneOffset()) * 60 * 1000;
    let day = Math.floor(diff / 86400000) % 3;
    console.log(day);
    return day + 2;
  }
  public x=this.getDayOfYear(this.getDate());
  guess = 0;
 //for guess 1 --------------------------------------------------------------------------------------------------
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
//for guess 2 ------------------------------------------------------------------------------------------------------------

checkStreet3(k: any, j: any): boolean{
    if (j.includes(k)){
      this.bgcolor3 = "#80ff80";
      return true;
    }
    else{
      this.bgcolor3 = "#ff8080";
      return false;
    }
  }

  checkStreet4(k: any, j: any): boolean{
    if (j.includes(k)){
      this.bgcolor4 = "#80ff80";
      return true;
    }
    else{
      this.bgcolor4 = "#ff8080";
      return false;
    }
  }

 //for guess 3 ------------------------------------------------------------------------------------------------------------

checkStreet5(k: any, j: any): boolean{
    if (j.includes(k)){
      this.bgcolor5 = "#80ff80";
      return true;
    }
    else{
      this.bgcolor5 = "#ff8080";
      return false;
    }
  }

  checkStreet6(k: any, j: any): boolean{
    if (j.includes(k)){
      this.bgcolor6 = "#80ff80";
      return true;
    }
    else{
      this.bgcolor6 = "#ff8080";
      return false;
    }
  } 
//final checking function (not used rn)-------------------------------------------------------------------------------------
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
  //cookie functions------------------------------------------------------------------------------------------------------------
  mounted() {
    //for guess 1
    if (localStorage.street1) {
      this.selectedStreet1 = localStorage.street1;
    }
    if (localStorage.street2) {
      this.selectedStreet2 = localStorage.street2;
    }

    if (localStorage.guess1Selected) {
      this.guess1Selected = localStorage.guess1Selected;
    }

    //for guess 2
    if (localStorage.street3) {
      this.selectedStreet3 = localStorage.street3;
    }
    if (localStorage.street4) {
      this.selectedStreet4 = localStorage.street4;
    }
   
    if (localStorage.guess2Selected) {
      this.guess2Selected = localStorage.guess2Selected;
    }

    //for guess 3
    if (localStorage.street5) {
      this.selectedStreet5 = localStorage.street5;
    }
    if (localStorage.street6) {
      this.selectedStreet6 = localStorage.street6;
    }
   
    if (localStorage.guess3Selected) {
      this.guess3Selected = localStorage.guess3Selected;
    }

    //saving colors--------------------------------------------------------------------------------------------
    //guess 1
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

    //guess 2
    if (localStorage.guess2street1 === "true") {
      this.bgcolor3 = "#80ff80";
    } else if (localStorage.guess2street1 === "false") {
      this.bgcolor3 = "#ff8080";
    } else {
      this.bgcolor3 = "white";
    }
    if (localStorage.guess2street2 === "true") {
      this.bgcolor4 = "#80ff80";
    } else if (localStorage.guess2street2 === "false") {
      this.bgcolor4 = "#ff8080";
    } else {
      this.bgcolor4 = "white";
    }

    //guess 3
    if (localStorage.guess3street1 === "true") {
      this.bgcolor5 = "#80ff80";
    } else if (localStorage.guess3street1 === "false") {
      this.bgcolor5 = "#ff8080";
    } else {
      this.bgcolor5 = "white";
    }
    if (localStorage.guess3street2 === "true") {
      this.bgcolor6 = "#80ff80";
    } else if (localStorage.guess3street2 === "false") {
      this.bgcolor6 = "#ff8080";
    } else {
      this.bgcolor6 = "white";
    }

  }


  // setting guesses----------------------------------------------------------------------------------------------------------------
  //first attempt
  setFirstGuess(street1: string, street2: string) {
    if (street1 != street2 && street1 != "" && street2 != "" && this.allStreets.includes(street1) && this.allStreets.includes(street2)){
    localStorage.guess1street1 = this.checkStreet1(street1, this.allCorners[this.x])
    localStorage.guess1street2 = this.checkStreet2(street2, this.allCorners[this.x])
    localStorage.street1 = street1;
    localStorage.street2 = street2;
    this.guess1Selected = true;
    localStorage.guess1Selected = this.guess1Selected;
    this.disabled1 = false;
    this.disabled2 = false;
    } else {
      if (street1 == "" || !this.allStreets.includes(street1)) {
        this.disabled1 = true;
      }
      if (street2 == "" || !this.allStreets.includes(street2)) {
        this.disabled2 = true;
      }
      if (street1 == street2) {
        this.disabled1 = true;
        this.disabled2 = true;
      }
    }
  }
  //second attemp
  setSecondGuess(street3: string, street4: string) {
   
    if (street3 != street4 && street3 != "" && street4 != "" && this.allStreets.includes(street3) && this.allStreets.includes(street4)){
    localStorage.guess2street1 = this.checkStreet3(street3, this.allCorners[this.x])
    localStorage.guess2street2 = this.checkStreet4(street4, this.allCorners[this.x])
    localStorage.street3 = street3;
    localStorage.street4 = street4;
    this.guess2Selected = true;
    localStorage.guess2Selected = this.guess2Selected;
    }
  }
//second attemp
setThirdGuess(street5: string, street6: string) {
   
   if (street5 != street6 && street5 != "" && street6 != "" && this.allStreets.includes(street5) && this.allStreets.includes(street6)){
   localStorage.guess3street1 = this.checkStreet5(street5, this.allCorners[this.x])
   localStorage.guess3street2 = this.checkStreet6(street6, this.allCorners[this.x])
   localStorage.street5 = street5;
   localStorage.street6 = street6;
   this.guess3Selected = true;
   localStorage.guess3Selected = this.guess3Selected;
   }
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



/* CSS */
.buttonG1 {
  
  background: #fa9a4c;
  border: 1px solid #fa9a4c;
  border-radius: 6px;
  box-shadow: rgba(224, 97, 11, 0.274) 1px 2px 4px;
  box-sizing: border-box;
  color: #FFFFFF;
  cursor: pointer;
  display: inline-block;
  font-family: nunito,roboto,proxima-nova,"proxima nova",sans-serif;
  font-size: 16px;
  font-weight: 800;
  line-height: 16px;
  min-height: 40px;
  outline: 0;
  padding: 12px 14px;
  text-align: center;
  text-rendering: geometricprecision;
  text-transform: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  vertical-align: middle;
}

.buttonG1:hover,
.buttonG1:active {
  background-color: initial;
  background-position: 0 0;
  color: #fa9a4c;
}

.buttonG1:active {
  opacity: 0;
}

.tt{
  
  border: 1px solid #ffffff;
  border-radius: 6px;
  box-shadow: rgba(109, 95, 86, 0.274) 1px 2px 4px;
  box-sizing: border-box;
  cursor: pointer;
  display: inline-block;
  font-family: nunito,roboto,proxima-nova,"proxima nova",sans-serif;
  font-size: 13px;
  font-weight: 1000;
  line-height: 16px;
  min-height: 40px;
  outline: 0;
  padding: 12px 14px;
  text-align: center;
  text-rendering: geometricprecision;
  text-transform: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  vertical-align: middle;
}

.shake {
  animation: shake 0.3s ease-in-out 0s 2;
  /* animation: shake 0.5s cubic-bezier(.36,.07,.19,.97) both;
  transform: translate3d(0, 0, 0);
  backface-visibility: hidden;
  perspective: 1000px; */
}
@keyframes shake {
  0% { margin-left: 0rem; }
  25% { margin-left: 0.5rem; }
  75% { margin-left: -0.5rem; }
  100% { margin-left: 0rem; }
}

.redoutline {
  box-shadow: 0 0 0.5em red;
}

</style>
<!-- #80ff80 -->
<!-- #ff8080 -->