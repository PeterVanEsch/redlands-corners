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
      <label style="font-size: 30px; font-family:Georgia, serif"> + </label>
      <div class="input-container">
        <input  class="tt" :class="{redoutline: disabled2}" type="search" @change="disabled2=false" placeholder="Second street" list="data" v-model="selectedStreet2" :disabled="guess1Selected" :style="{'background-color':bgcolor2}"/>
        <datalist id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
        <button class="buttonG1" @click="setFirstGuess(selectedStreet1, selectedStreet2)" >Guess</button>
      </div>
    </center>
    <br>
    <center :class="{shake: disabled3 || disabled4}">
      <div class="input-container">
        <input  class="tt" :class="{redoutline: disabled3}" type="search" @change="disabled3=false" placeholder="First street" list="data" v-model="selectedStreet3" :disabled="guess2Selected || !guess1Selected" :style="{'background-color':bgcolor3}"/>
        <datalist id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
      </div>
      <img alt="and" src="../assets/potenialPLus.png" height="30" width="30" >
      <div class="input-container">
        <input class="tt" :class="{redoutline: disabled4}" type="search"  @change="disabled4=false" placeholder="Second street" list="data" v-model="selectedStreet4" :disabled="guess2Selected || !guess1Selected" :style="{'background-color':bgcolor4}"/>
        <datalist  id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
        <button class="buttonG1" @click="setSecondGuess(selectedStreet3, selectedStreet4)" >Guess</button>
      </div>
    </center>
    <br>
    <center :class="{shake: disabled5 || disabled6}">
      <div class="input-container">
        <input  class="tt" :class="{redoutline: disabled5}" type="search"  @change="disabled5=false" placeholder="First street" list="data" v-model="selectedStreet5" :disabled="guess3Selected || !guess2Selected" :style="{'background-color':bgcolor5}"/>
        <datalist id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
      </div>
      <label> and </label>
      <div class="input-container">
        <input class="tt" :class="{redoutline: disabled6}" type="search"   @change="disabled6=false" placeholder="Second street" list="data" v-model="selectedStreet6" :disabled="guess3Selected || !guess2Selected" :style="{'background-color':bgcolor6}"/>
        <datalist  id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
        <button class="buttonG1" @click="setThirdGuess(selectedStreet5, selectedStreet6)" >Guess</button>
      </div>
    </center>
      <br>
    <center :class="{shake: disabled7 || disabled8}">
      <div class="input-container">
        <input  class="tt" :class="{redoutline: disabled7}" type="search"  @change="disabled7=false" placeholder="First street" list="data" v-model="selectedStreet7" :disabled="guess4Selected || !guess3Selected" :style="{'background-color':bgcolor7}"/>
        <datalist id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
      </div>
      <label> and </label>
      <div class="input-container">
        <input class="tt" :class="{redoutline: disabled8}" type="search"   @change="disabled8=false" placeholder="Second street" list="data" v-model="selectedStreet8" :disabled="guess4Selected || !guess3Selected" :style="{'background-color':bgcolor8}"/>
        <datalist  id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
        <button class="buttonG1" @click="setForthGuess(selectedStreet7, selectedStreet8)" >Guess</button>
      </div>
      <h1>{{ guessCount }}</h1>
      <h1> {{ totalStars }}</h1>
      <!--<h1>{{ totalGuesses }}</h1>-->
      <h1>{{ totalDays }}</h1>
    </center>
    <div class="winz" v-if="gameWon && yesDisplay">
      <button class="close" @click="yesDisplay=false">X</button>
      <center><h1>{{ congratsMSG[guessCount-1][congratsIndex] }}</h1></center>
      <center><div class="rating">
  <span class="star" v-if="5 - guessCount + 1 >= 1"  ></span>
  <span class="star"  v-if="5 - guessCount + 1 >= 2"></span>
  <span class="star" v-if="5 - guessCount + 1 >= 3"></span>
  <span class="star" v-if="5 - guessCount + 1 >= 4"></span>
  <span class="star" v-if="5 - guessCount + 1 >= 5"></span>
  
</div></center>
<center><h1 v-if="guessCount==1" class="winMsg" >  You got it in 1 guess</h1></center>
  <center><h1 v-if="guessCount!=1" class="winMsg">You got it in {{ guessCount }} guesses</h1></center>
  <br>
  <br>
  <center><h1 class="avgMsg">Average score: {{ Math.round(totalStars/totalDays*100)/100 }} <img alt="stars" src="../assets/star.jpg" height="20" width="20" ></h1></center>
    </div>

  <div class="loss" v-if="!gameWon && guessCount == 4 && yesDisplay">
    <button class="close" @click="yesDisplay=false">X</button>
    <center><h1> {{ lozeMSg[congratsIndex] }}</h1></center>
    <center><h1 class="winMsg"> The correct answer was {{ allCorners[x][0] }} and  {{ allCorners[x][1] }}</h1></center>
  </div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
@Options({
  watch: {
    gameWon(toSet) {localStorage.gameWon = toSet;},
    guess1Selected(toSet) {
      localStorage.guess1Selected = toSet;},
    guess2Selected(toSet) {localStorage.guess2Selected = toSet;},
    guess3Selected(toSet) {localStorage.guess3Selected = toSet;},
    guess4Selected(toSet) {localStorage.guess4Selected = toSet;},
    guessCount(toSet) {localStorage.guessCount = toSet;},
    // totalGuesses(toSet) {localStorage.totalGuesses = toSet;},
    totalStars(toSet) {localStorage.totalStars = toSet;},
    totalDays(toSet) {localStorage.totalDays = toSet;},
  }
})
export default class Home extends Vue {
  // Lists used for all program-----------------------------------------------------------------------------------------------
  public allStreets = ['1st', 'Gavin', 'Maple', 'Olive', 'Pine', 'Redlands', 'San Mateo', "wrong", "answer", "still", "incorrect", "what", "the", "ryan", "is", "so", "dumb", "Palm", "S Buena Vista St", "W Clark st", "S Michigan st"];
  public allCorners = [["madeup",  "test"] , ["wrong", "answer"], ["still", "incorrect"], ["cant", "remember"], ["more", "needed"], ["Palm", "S Buena Vista St"] , ["W Clark st", "S Michigan st"] ];
  public allHouse = [1,2,3,4,5,6];

  public gameWon = false;
  public yesDisplay = true;
  public congratsMSG = [["Amazing", "Brilliant", "Perfect", "Astounding", "Ingenius"], ["Congrats", "Great Playing", "Superb", "Too Easy"], ["Not Bad", "Good Game", "Not to shabby", "Well Done"], ["Acceptable", "Not the worst", "Could be better", "Mediocre"]];
  public lozeMSg = ["Sorry You Lost", "OH NO!", "Game Over", "Better Luck Tomorrow"];
  public congratsIndex = Math.floor(Math.random() * 4);

  //all the stars 
  public totalStars = 0;
  public totalDays = 0;
  // public totalGuesses = 0;
  // orgininally setting players 5 guessses----------------------------------------------------------------------------------
  //first guess 
  public selectedStreet1 = '';
  public selectedStreet2 = '';
  public guess1Selected = false;
  public bgcolor1 = "white";
  public bgcolor2 = "white";
  public disabled1 = false;
  public disabled2 = false;
  //second guess
  public selectedStreet3 = '';
  public selectedStreet4 = '';
  public guess2Selected = false;
  public bgcolor3 = "white";
  public bgcolor4 = "white";
  public disabled3 = false;
  public disabled4 = false;
  //third guess
  public selectedStreet5 = '';
  public selectedStreet6 = '';
  public guess3Selected = false;
  public bgcolor5 = "white";
  public bgcolor6 = "white";
  public disabled5 = false;
  public disabled6 = false;
  //forth guess
  public selectedStreet7 = '';
  public selectedStreet8 = '';
  public guess4Selected = false;
  public bgcolor7 = "white";
  public bgcolor8 = "white";
  public disabled7 = false;
  public disabled8 = false;

  public guessCount = 0;
  
  //date functions-------------------------------------------------------------------------------------------------------------------
  getDate() {
    return new Date();
  }
  getDayOfYear(date: Date) {
    let start = new Date(date.getFullYear(), 0, 0);
    let diff = date.getTime() - start.getTime() + (start.getTimezoneOffset() - date.getTimezoneOffset()) * 60 * 1000;
    let day = Math.floor(diff / 86400000) % 3;
    return day + 2;
  }

  public x =  /*this.getDayOfYear(this.getDate());*/ 5;

  checkDay(){
    return localStorage.Day == this.getDayOfYear(this.getDate());
  }

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


   //for guess 3 ------------------------------------------------------------------------------------------------------------

  checkStreet7(k: any, j: any): boolean{
    if (j.includes(k)){
      this.bgcolor7 = "#80ff80";
      return true;
    }
    else{
      this.bgcolor7 = "#ff8080";
      return false;
    }
  }

  checkStreet8(k: any, j: any): boolean{
    if (j.includes(k)){
      this.bgcolor8 = "#80ff80";
      return true;
    }
    else{
      this.bgcolor8 = "#ff8080";
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
        return "you got the right corner in " + this.guessCount + "attempts";
      }
      else{
        return "you got the wrong corner";
      }
      
    }
  }
  //cookie functions------------------------------------------------------------------------------------------------------------
  mounted() {
    if (!this.checkDay()){
        localStorage.guessCount = 0;
        localStorage.guess1Selected = false;
        localStorage.guess2Selected = false;
        localStorage.guess3Selected = false;
        localStorage.guess4Selected = false;
        localStorage.gameWon = false;
        localStorage.Day = this.getDayOfYear(this.getDate());

        localStorage.guess1street1 = null;
        localStorage.guess1street2 = null;
        localStorage.street1 = '';
        localStorage.street2 = '';
        

        localStorage.guess2street1 = null;
        localStorage.guess2street2 = null;
        localStorage.street3 = '';
        localStorage.street4 = '';

        localStorage.guess3street1 = null;
        localStorage.guess3street2 = null;
        localStorage.street5 = '';
        localStorage.street6 = '';

        localStorage.guess4street1 = null;
        localStorage.guess4street2 = null;
        localStorage.street7 = '';
        localStorage.street8 = '';
    }

    if (localStorage.totalStars) {
      this.totalStars = parseInt(localStorage.totalStars);
    }
    if (localStorage.totalDays) {
      this.totalDays = parseInt(localStorage.totalDays);
    }
    //save total guesses
    // if (localStorage.totalGuesses){
    //   this.totalGuesses = parseInt(localStorage.totalGuesses);
    // }
    if (localStorage.guessCount) {
      this.guessCount = parseInt(localStorage.guessCount);
    }
    if (localStorage.gameWon != null) {
      this.gameWon = localStorage.gameWon === "true";
    }
   
    //for guess 1
    if (localStorage.street1) {
      this.selectedStreet1 = localStorage.street1;
    }
    if (localStorage.street2) {
      this.selectedStreet2 = localStorage.street2;
    }

    if (localStorage.guess1Selected != null) {
      this.guess1Selected = localStorage.guess1Selected === "true";
    }
  
    //for guess 2
    if (localStorage.street3) {
      this.selectedStreet3 = localStorage.street3;
    }
    if (localStorage.street4) {
      this.selectedStreet4 = localStorage.street4;
    }
   
    if (localStorage.guess2Selected != null) {
      this.guess2Selected = localStorage.guess2Selected === "true";
    }

    //for guess 3
    if (localStorage.street5) {
      this.selectedStreet5 = localStorage.street5;
    }
    if (localStorage.street6) {
      this.selectedStreet6 = localStorage.street6;
    }
   
    if (localStorage.guess3Selected != null) {
      this.guess3Selected = localStorage.guess3Selected === "true";
    }

    //for guess 4
    if (localStorage.street7) {
      this.selectedStreet7 = localStorage.street7;
    }
    if (localStorage.street8) {
      this.selectedStreet8 = localStorage.street8;
    }
   
    if (localStorage.guess4Selected != null) {
      this.guess4Selected = localStorage.guess4Selected === "true";
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

    //guess 4
    if (localStorage.guess4street1 === "true") {
      this.bgcolor7 = "#80ff80";
    } else if (localStorage.guess4street1 === "false") {
      this.bgcolor7 = "#ff8080";
    } else {
      this.bgcolor7 = "white";
    }
    if (localStorage.guess4street2 === "true") {
      this.bgcolor8 = "#80ff80";
    } else if (localStorage.guess4street2 === "false") {
      this.bgcolor8 = "#ff8080";
    } else {
      this.bgcolor8 = "white";
    }

  }


  // setting guesses----------------------------------------------------------------------------------------------------------------
  //first attempt
  setFirstGuess(street1: string, street2: string) {
    if (street1 != street2 && street1 != "" && street2 != "" && this.allStreets.includes(street1) && this.allStreets.includes(street2)) {
      let s1 = this.checkStreet1(street1, this.allCorners[this.x]);
      let s2 = this.checkStreet2(street2, this.allCorners[this.x]);
      localStorage.guess1street1 = s1;
      localStorage.guess1street2 = s2;
      if (!this.guess1Selected){
        this.guessCount += 1;
        // this.totalGuesses += 1;
        this.totalDays++;
      }
      if (s1 && s2){
        this.gameWon = true;
        this.guess2Selected = true;
        this.guess3Selected = true;
        this.guess4Selected = true;
        if (!this.guess1Selected){
          this.totalStars += 5;
        }
      }
      localStorage.street1 = street1;
      localStorage.street2 = street2;

      this.guess1Selected = true;
      
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
    let s1 = this.checkStreet3(street3, this.allCorners[this.x]);
    let s2 = this.checkStreet4(street4, this.allCorners[this.x]);
    localStorage.guess2street1 = s1;
    localStorage.guess2street2 = s2;
    if (!this.guess2Selected){
      this.guessCount += 1;
      // this.totalGuesses += 1;
    }
    if (s1 && s2){
      this.gameWon = true;
      this.guess3Selected = true;
      this.guess4Selected = true;
      if (!this.guess2Selected){
        this.totalStars += 4;
      }
    }
    localStorage.street3 = street3;
    localStorage.street4 = street4;
    this.guess2Selected = true;
    this.disabled3 = false;
    this.disabled4 = false;
    }else {
      if (street3 == "" || !this.allStreets.includes(street3)) {
        this.disabled3 = true;
      }
      if (street4 == "" || !this.allStreets.includes(street4)) {
        this.disabled4 = true;
      }
      if (street3 == street4) {
        this.disabled3 = true;
        this.disabled4 = true;
      }
    }
  }
//third attempt
setThirdGuess(street5: string, street6: string) {
   
  if (street5 != street6 && street5 != "" && street6 != "" && this.allStreets.includes(street5) && this.allStreets.includes(street6)){
  let s1 = this.checkStreet5(street5, this.allCorners[this.x]);
  let s2 = this.checkStreet6(street6, this.allCorners[this.x]);
  localStorage.guess3street1 = s1;
  localStorage.guess3street2 = s2;
   if (!this.guess3Selected){
      this.guessCount += 1;
      // this.totalGuesses += 1;
    }
   if (s1 && s2){
      this.gameWon = true;
      this.guess4Selected = true;
      if (!this.guess3Selected){
        this.totalStars += 3;
      }
    }
   localStorage.street5 = street5;
   localStorage.street6 = street6;
   this.guess3Selected = true;
   this.disabled5 = false;
   this.disabled6 = false;
   }
   else {
      if (street5 == "" || !this.allStreets.includes(street5)) {
        this.disabled5 = true;
      }
      if (street6 == "" || !this.allStreets.includes(street6)) {
        this.disabled6 = true;
      }
      if (street5 == street6) {
        this.disabled5 = true;
        this.disabled6 = true;
      }
    }
 }

 setForthGuess(street7: string, street8: string) {
   
  if (street7 != street8 && street7 != "" && street8 != "" && this.allStreets.includes(street7) && this.allStreets.includes(street8)){
  let s1 = this.checkStreet7(street7, this.allCorners[this.x]);
  let s2 = this.checkStreet8(street8, this.allCorners[this.x]);
  localStorage.guess4street1 = s1;
  localStorage.guess4street2 = s2;
   if (!this.guess4Selected){
      this.guessCount += 1;
      // this.totalGuesses += 1;
    }
   if (s1 && s2){
      this.gameWon = true;
      if (!this.guess4Selected){
        this.totalStars += 2;
      }
    }
   localStorage.street7 = street7;
   localStorage.street8 = street8;
   this.guess4Selected = true;
   this.disabled7 = false;
   this.disabled8 = false;
   }
   else {
      if (street7 == "" || !this.allStreets.includes(street7)) {
        this.disabled7 = true;
      }
      if (street8 == "" || !this.allStreets.includes(street8)) {
        this.disabled8 = true;
      }
      if (street7 == street8) {
        this.disabled7 = true;
        this.disabled8 = true;
      }
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

.winz{
  z-index: 4;
  position: absolute;
  font-size: 30px;
  font-family: nunito,roboto,proxima-nova,"blippo", fantasy;
  background-color: rgb(241, 252, 241);
  color: #fa9a4c;
  border-radius: 20px;
  width: 500px;
  height: 500px;
  border: 0px solid #a09f9f;
  box-shadow: 0 0 0.9em rgb(161, 253, 143);
  top: 10%;
  
}
.loss{
  z-index: 4;
  position: absolute;
  font-size: 30px;
  font-family: nunito,roboto,proxima-nova,"blippo", fantasy;
  background-color: rgb(241, 252, 241);
  color: #fa9a4c;
  top: 10%;
  left: 35%;
  border-radius: 20px;
  width: 500px;
  height: 500px;
  border: 0px solid #a09f9f;
  box-shadow: 0 0 0.9em rgb(161, 253, 143);
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

.rating {
  display: inline-block;
  font-size: 0;
}

.winMsg{
  font-size: 85%;
  font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif
}

.star {
  display: inline-block;
  width: 60px;
  height: 60px;
  background-image: url("../assets/star.jpg");
  background-repeat: no-repeat;
  background-size: contain;
  opacity: 0;
  transition: opacity .8s ease-in-out;
}

.star:nth-child(1) {
  animation: showStar 1s .5s forwards;
}

.star:nth-child(2) {
  animation: showStar 1s 1s forwards;
}

.star:nth-child(3) {
  animation: showStar 1s 1.5s forwards;
}

.star:nth-child(4) {
  animation: showStar 1s 2s forwards;
}

.star:nth-child(5) {
  animation: showStar 1s 2.5s forwards;
}

@keyframes showStar {
  from { opacity: 0; }
  to { opacity: 1; }
}

.close{
  background-color: rgb(241, 252, 241);
  float: right;
  border: 0px;
  font-size: 30px;
  font-family: Consolas, monaco, monospace;
  padding: 2%;
}

.avgMsg{
  font-family: Consolas, monaco, monospace;
  font-size: 55%;
  color: rgb(85, 85, 85);
}
</style>
<!-- #80ff80 -->
<!-- #ff8080 -->