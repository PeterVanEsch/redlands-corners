<template>
  <div class="home">
    <center><img alt="My logo" src="../assets/logo.png" height="75" width="450"></center>
    <br>
    <center><img alt="My house" v-bind:src="require(`../assets/h${x}.jpg`)" height="300" width="500"></center>

    <div class="input-container">
    <label for="street1"> first street:</label>
    
    <input type="text" id="street1" v-model="userInput1" :disabled="street1Selected">
    
    <select v-model="selectedStreet1" @change="onStreet1Selected">
      <option v-for="street in filteredStreets1" :disabled="street1Selected" @change="onStreet1Selected" :key="street">{{ street }} </option>
    </select>
    </div>
    <div class="input-container">

    <label for="street2" >  second street:</label>
    <input type="text" id="street2" v-model="userInput2" :disabled="street2Selected">
    <select v-model="selectedStreet2"  @change="onStreet2Selected">
      <option v-for="street in filteredStreets2" :disabled="street2Selected" @change="onStreet2Selected" :key="street">{{ street }}</option>
    </select>
  </div>
<br>
<br>
  <div class="input2-container">
    <label for="street3"> first street:</label>
    
    <input type="text" id="street3" v-model="userInput3" :disabled="street3Selected">
    
    <select v-model="selectedStreet3" @change="onStreet3Selected">
      <option v-for="street in filteredStreets3" :disabled="street3Selected" @change="onStreet3Selected" :key="street">{{ street }} </option>
    </select>
    </div>
    <div class="input2-container">

    <label for="street4" >  second street:</label>
    <input type="text" id="street4" v-model="userInput4" :disabled="street4Selected">
    <select v-model="selectedStreet4"  @change="onStreet4Selected">
      <option v-for="street in filteredStreets4" :disabled="street4Selected" @change="onStreet4Selected" :key="street">{{ street }}</option>
    </select>
  </div>

    <h2><center>{{ selectedStreet1 }}</center></h2>
    <h2><center>{{ selectedStreet2 }}</center></h2>
    <h2>{{ checkName(selectedStreet1,allCorners[x]) }} </h2>
    <h2>{{ checkName(selectedStreet2,allCorners[x]) }} </h2>
    <h2>{{ finalCheck(selectedStreet1, selectedStreet2, allCorners[x]) }}</h2>
    
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
  public street1Selected = false;
  public street2Selected = false;
  //second guess
  public userInput3 = '';
  public selectedStreet3 = '';
  public userInput4 = '';
  public selectedStreet4 = '';
  public street3Selected = false;
  public street4Selected = false;

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

  x = this.getDayOfYear(this.getDate());
  guess = 0;

  //selectring steets to diable after click---------------------------------------------------------------------------------------
  //first guess
  onStreet1Selected() {
    this.street1Selected = true;
    
  }
  onStreet2Selected(){
    this.street2Selected = true;
    this.guess += 1;
  }
  //second guess
  onStreet3Selected() {
    this.street3Selected = true;
    
  }
  onStreet4Selected(){
    this.street4Selected = true;
    this.guess += 1;
  }
 
  checkName(k: any, j: any){
    if (j.includes(k)){
      return "correct";
    }
    else{
      return "incorrect"
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
  

  //public score = /*this.allCorners[this.x].includes(this.selectedStreet1)*/ this.checkName(this.selectedStreet1, this.allCorners[this.x],);

  getDayOfYear(date: Date) {
    let start = new Date(date.getFullYear(), 0, 0);
    let diff = date.getTime() - start.getTime() + (start.getTimezoneOffset() - date.getTimezoneOffset()) * 60 * 1000;
    let day = Math.floor(diff / 86400000);
    return day;
  }
}
</script>

<style scoped>
.input-container{
  display: inline-block; 
}
.input2-container{
  display: inline-block;  
  
}

 .incorrect-input {
  background-color: #ff8080;
}

.correct-input {
  background-color: #80ff80;
}
</style>
