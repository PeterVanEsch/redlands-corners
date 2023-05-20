<template>
  <div class="home">
    <center>
      <img alt="My logo" src="../assets/better.png" height="210" width="406" >
    </center>
    <br>
    <center>
      <img alt="My house" v-bind:src="require(`../assets/h${x}.jpg`)" height="300" width="500" style="border: 6px solid #000000; padding: 10px; margin: 5px;">
    </center>
    <center :class="{shake: disabled1 || disabled2}">
      <div class="guess1">
      <div class="input-container">
        <input class="tt" :class="{redoutline: disabled1}" type="search" @change="disabled1=false" placeholder="First street" list="data" v-model="selectedStreet1" :disabled="guess1Selected" :style="{backgroundColor: bgcolor1}"/>
        <datalist id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
      </div>
      <label style="font-size: 30px; font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif"> + </label>
      <div class="input-container">
        <input  class="tt" :class="{redoutline: disabled2}" type="search" @change="disabled2=false" placeholder="Second street" list="data" v-model="selectedStreet2" :disabled="guess1Selected" :style="{'background-color':bgcolor2}"/>
        <datalist id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
        <button class="buttonG1" @click="setFirstGuess(selectedStreet1, selectedStreet2)" >Guess</button>
      </div>
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
      <label style="font-size: 30px; font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif"> + </label>
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
      <label style="font-size: 30px; font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif"> + </label>
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
      <label style="font-size: 30px; font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif"> + </label>
      <div class="input-container">
        <input class="tt" :class="{redoutline: disabled8}" type="search"   @change="disabled8=false" placeholder="Second street" list="data" v-model="selectedStreet8" :disabled="guess4Selected || !guess3Selected" :style="{'background-color':bgcolor8}"/>
        <datalist  id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
        <button class="buttonG1" @click="setForthGuess(selectedStreet7, selectedStreet8)" >Guess</button>
      </div>
      </center>
      <br>
    <center :class="{shake: disabled9 || disabled10}">
      <div class="input-container">
        <input  class="tt" :class="{redoutline: disabled9}" type="search"  @change="disabled9=false" placeholder="First street" list="data" v-model="selectedStreet9" :disabled="guess5Selected || !guess4Selected" :style="{'background-color':bgcolor9}"/>
        <datalist id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
      </div>
      <label style="font-size: 30px; font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif"> + </label>
      <div class="input-container">
        <input class="tt" :class="{redoutline: disabled10}" type="search"   @change="disabled10=false" placeholder="Second street" list="data" v-model="selectedStreet10" :disabled="guess5Selected || !guess4Selected" :style="{'background-color':bgcolor10}"/>
        <datalist  id="data">
          <option v-for="item in allStreets" :key="item" :value="item"></option>
        </datalist>
        <button class="buttonG1" @click="setFifthGuess(selectedStreet9, selectedStreet10)" >Guess</button>
      </div>
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

  <div class="loss" v-if="!gameWon && guessCount == 5 && yesDisplay">
    <button class="close" @click="yesDisplay=false">X</button>
    <center><h1> {{ lozeMSg[congratsIndex] }}</h1></center>
    <center><h1 class="winMsg"> The correct answer was {{ allCorners[x][0] }} and  {{ allCorners[x][1] }}</h1></center>
    <br>
    <br>
    <center><h1 class="avgMsg">Average score: {{ Math.round(totalStars/totalDays*100)/100 }} <img alt="stars" src="../assets/star.jpg" height="20" width="20" ></h1></center>
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
    guess5Selected(toSet) {localStorage.guess5Selected = toSet;},
    guessCount(toSet) {localStorage.guessCount = toSet;},
    // totalGuesses(toSet) {localStorage.totalGuesses = toSet;},
    totalStars(toSet) {localStorage.totalStars = toSet;},
    totalDays(toSet) {localStorage.totalDays = toSet;},
  }
})
export default class Home extends Vue {

  public w = window.innerWidth;
  public h = window.innerHeight;
  // Lists used for all program-----------------------------------------------------------------------------------------------
  public allStreets = ['3rd Avenue','3rd Street','5th Avenue','5th Street','6th Avenue','6th Street','7Th Avenue','7th Place','7th Street','8th Street','9th Street','10th Street','11th Street','16th Street','17th Street','18th Street','A Street','Aaron Drive','Abbey Way','Acacia Court','Adams Street','Afton Court','Alabama Street','Alden Court','Alden Road','Alessandro Road','Allison Way','Almond Avenue','Alpine Court','Alta Loma Drive','Alta Mira Drive','Alta Mira Place','Alta Street','Alta Vista Drive','Alvarado Street','Amapolas Street','Amber Court','Amherst Court','Amigos Drive','Anita Court','Anthony Street','Arbor Drive','Arcata Drive','Ardmore Avenue','Ardmore Circle','Ardmore Court','Arizona Street','Arlene Street','Arrowview Drive','Arroyo Crst','Arroyo Road','Ashforth Drive','Ashley Way','Auburn Court','Austin Way','Avenue N','Aviation Drive','Azalea Court','B Street','Balboa Court','Baldwin Avenue','Balfour Court','Banyan Drive','Bar Ru Lane','Barbra Lane','Barrington Circle','Barton Road','Beattie Lane','Beaumont Avenue','Beauregard Court','Bedford Drive','Begonia Court','Belinda Lane','Bella Vista Court','Bella Vista Crst','Bellevue Avenue','Bellevue Court','Bellevue Road','Belmont Court','Benbow Place','Benita Marie Crst','Berkeley Drive','Bermuda Drive','Bermudez Street','Beryl Avenue','Beverly Drive','Birch Court','Black Hawk Court','Blossom Avenue','Blossom Court','Blue Bird Lane','Blue Jay Lane','Blue Wing Court','Bond Street','Bone Drive','Bonita Street','Bow B Street','Bow C Street','Bradbury Drive','Bradford Place','Brandon Court','Brandon Street','Brentwood Place','Brewster Way','Brian Court','Brigette Court','Brighton Court','Brittany Drive','Brookdale Drive','Brookside Avenue','Brookstone Street','Bruder Lane','Bryn Mawr Avenue','Buckeye Street','Buckingham Drive','Buffalo Meadows Road','Burgis Street','Burke Street','Burns Lane','Burnt Mill Canyon Road','Bus Center Court','Bus Center Drive','Caballero Lane','Cajon Street','Calhoun Street','California Street','Calvary Circle','Cam Real','Cambon Court','Cambria Court','Cambridge Avenue','Cambridge Circle','Camelot Drive','Cameo Drive','Campbell Avenue','Campus Avenue','Candela Street','Candy Lane','Cantania Avenue','Canterbury Circle','Canyon Oaks Drive','Canyon Road','Canyon View Lane','Capri Avenue','Cardigan Place','Cardinal Lane','Carlotta Court','Carlson Avenue','Carmel Court','Carmody Court','Carmody Street','Carnes Circle','Carob Street','Carrie Lane','Carver Circle','Carver Drive','Casa de Leon','Cascade Court','Cascade Street','Cascante Court','Castlegate Lane','Cave Street','Cedar Avenue','Center Crest Drive','Central Avenue','Century Street','Cero Court','Channing Street','Chaparral Drive','Chapel Street','Chapparal Road','Charline Avenue','Chaucer Court','Chelsea Avenue','Cheryl Street','Chestnut Avenue','Cheyene Street','Cheyenne Way','Chisholm Trail','Christopher Lane','Chula Vista Street','Church Place','Church Street','Cimarron Court','Cimarron Drive','Circle Drive','Circle Terrace','Citrus Avenue','Clay Street','Clifton Avenue','Clifton Court','Cll Constancia','Cll de Acacia','Cll de Barranca','Cll de Silva','Cll Solejar','Clock Avenue','Clock Street','Clover Street','Club Drive','Colgate Place','College Avenue','Colorado Street','Columbia Road','Columbia Street','Commerce Street','Concord Lane','Cone Camp Road','Conestoga Court','Conn Way','Cook Street','Copper Hill Lane','Coral Court','Cordova Avenue','Cornell Avenue','Coronado Drive','Corporate Drive','Cortez Street','Cottage Terrace','Coulston Avenue','Country Club Drive','Country Club Lane','Country Place','Country Road','Courier Avenue','Crafton Avenue','Crafton Court','Crafton Hills Drive','Crafton Pointe Drive','Crafts Estate Road','Craig Court','Creek View Lane','Creekside Drive','Crest Road','Crestview Road','Crestwood Drive','Crocus Street','Crown Street','Crystal Cove Court','Crystal Springs Lane','Cynthia Crst','Cypress Circle','Cypress Way','Daisy Avenue','Daisy Court','Dale Lane','Dalton Court','Dana Street','Danelaw Avenue','Darlene Court','Darlene Way','de Anza Street','Deadwood Court','Deanna Way','Dearborn Circle','Deer Trail Drive','Delaware Avenue','Denise Avenue','Deodar Street','Devon Place','Devonshire Drive','Dexter Way','Diamond Court','Division Street','Dolores Court','Domestic Avenue','Donna Drive','Dover Court','Doyle Avenue','Dracena Court','Drake Ridge Cres','Dreka Avenue','Dubois Street','Duke Street','Dwight Street','E 6th Avenue','E 11th Street','E Brockton Avenue','E Central Avenue','E Citrus Avenue','E Clark Street','E Colton Avenue','E Crescent Avenue','E Culvert Street','E Cypress Avenue','E Delaware Avenue','E Delhaven Court','E Fern Avenue','E Franklin Avenue','E Herrington Drive','E High Avenue','E Highland Avenue','E Hilton Avenue','E Home Place','E I 10 Oh S','E Lugonia Avenue','E Mariposa Drive','E Olive Avenue','E Orange Street','E Palm Avenue','E Palm Lane Drive','E Park Avenue','E Pearl Avenue','E Pennsylvania Avenue','E Pioneer Avenue','E Redlands Boulevard','E Rosette Street','E San Bernardino Avenue','E Sharon Road','E South Avenue','E State Street','E Stuart Avenue','E Sun Avenue','E Sunset Drive N','E Sunset Drive S','E Union Avenue','E Vine Street','E Western Avenue','E York Street','Eastbern Lane','Eastpark','Eastwood Street','Eddy Court','Edgehill Lane','Edgemont Drive','Edwards Street','Elder Road','Elder Way','Elise Drive','Elizabeth Crest Drive','Elizabeth Street','Elm Street','Elmwood Court','Emerald Avenue','Emery Court','Emilia Way','Emily Street','Endymion Way','Engman Road','Enterprise Drive','Entranz Boulevard','Escondido Road','Essex Court','Esther Way','Eucalyptus Drive','Evergreen Court','Everron Court','Fairmont Drive','Fairway Drive','Falcon Lane','Fallbrook Avenue','Fallbrook Court','Farview Lane','Fawn Court','Felisa Court','Ferndale Court','Fernwood Drive','Finch Avenue','Fletcher Avenue','Florida Street','Foothill Way','Ford Drive','Ford Street','Forest Court','Fountain Avenue','Fountain Drive','Fountain Lane','Fountain Place','Fountain Vw','Fountain Way','Fox Court','Frances Street','Franklin Avenue','Fremont Street','Freya Drive','Friar Lane','Frontage Road','Frontier Avenue','Fulbright Avenue','Fulbright Court','Furlow Drive','Gabrielle Way','Gail Avenue','Garden Hill Drive','Garden Street','Gardenia Avenue','Garfield Way','Gary Lane','Georgia Street','Gideon Way','Glen Haven Way','Glenn Court','Glenwood Drive','Glover Street','Gold Buckle Court','Gold Cup Court','Gold Hill Grade','Gold Hill Lane','Golden West Drive','Goldenrod Avenue','Granada Court','Grand View Drive','Granite Street','Grant Street','Greenbriar Court','Greenspot Road','Greenwood Court','Greystone Avenue','Grove Street','Halsey Street','Hamlin Place','Hampton Road','Hamstead Circle','Hanford Street','Harding Drive','Harp Place','Hartford Circle','Hartzell Avenue','Harvard Court','Hastings Street','Heath Street','Heather Lane','Heidi Court','Helen Court','Helen Drive','Helena Lane','Hemlock Court','Henrietta Street','Herald Street','Heritage Lane','Heron Court','Herrington Drive','Hibiscus Drive','Hidalgo Avenue','High Avenue','Highland Avenue','Highview Drive','Highview Lane','Hilary Lane','Hilary Way','Hillside Way','Hilltop Drive','Holly Lane','Home Place','Horse Trail Lane','Houston Way','Hubbard Court','Hugo Street','Hunter Drive','Hyacinth Avenue','Idaho Street','Idyllwild Court','Imperial Court','Independence Avenue','Independence Court','Indiana Court','Industrial Circle','Industrial Park Avenue','Interstate 10','Iowa Street','Iris Street','Irwin Court','Ivy Street','Jade Court','James Court','Jasmine Street','Jason Court','Jasper Avenue','Jean Avenue','Jefferson Street','Jennifer Street','Jesse Way','Joanne Street','Joni Lane','Jordan Drive','Juanita Lane','Judson Street','Julie Court','Juniper Court','Jurupa Avenue','Kansas Street','Karon Street','Kathi Street','Kaye Court','Kelisa Circle','Kelly Street','Kendall Street','Kendall Way','Kensington Drive','Kenwood Drive','Kevin Avenue','Kimball Lane','Kimberly Avenue','Kimberly Place','Kincaid Street','King Street','Kings Way','Kingsbury Drive','Kingston Circle','Kingswood Drive','Kirby Court','Klamath Street','Knightsbridge Lane','Knoll Drive','Knoll Road','Kristin Court','Kyle Lane','la Arriba Drive','la Colina Drive','la Cresta Drive','la Feliz Drive','la Flora Drive','la Hermosa Drive','la Loma Drive','la Mirada Drive','la Paloma Street','la Solana Court','la Solana Drive','la Verne Street','Ladera Street','Lake Drive','Lake Shore Drive','Lakeshore Drive','Lakeside Avenue','Lalania Avenue','Lanfair Street','Lantern Crest Drive','Laramie Avenue','Lassen Street','Laurel Avenue','Lawton Street','Lemon','Lemon Street','Lemonwood Avenue','Lexington Lane','Lido Street','Lilac Court','Lime','Lime Street','Linda Place','Linda Vista Avenue','Lindero Street','Lisa Lane','Lisa Marie Lane','Live Oak Canyon Road','Live Oak Court','Live Oak Cyn Road','Live Oak-Sunset Acrd','Lolita Avenue','Lomas Verdes Street','Lombard Drive','Longview Avenue','Lori Court','Los Altos Drive','Los Robles Crst','Lotus Avenue','Lotus Court','Lucy Street','Lugonia Avenue','Lupine Street','Lynne Court','Lytle Street','Madison Street','Magnolia Avenue','Manzanita Road','Maple Avenue','Marcia Street','Margarita Drive','Margit Street','Maria Court','Marian Avenue','Marigold Street','Marilyn Avenue','Marilyn Lane','Marion Road','Mariposa Drive','Marjorie Crst','Marshall Street','Marty Street','Marvin Avenue','Matthew Court','Mayflower Drive','Mc Kinley Drive','McAuliffe Court','McGehee Drive','Meadowbrook Lane','Medallion Street','Melbury Court','Melbury Place','Mendocino Way','Menlo Avenue','Merced Street','Mesa Drive','Mesa View Lane','Mia Court','Michael Court','Midway Street','Milburn Avenue','Mills Avenue','Mira Bella Court','Mira Monte Drive','Miradero Drive','Miradero Place','Miramonte Street','Mirasol Drive','Mission Road','Missouri Court','Mitchell Way','Mona Avenue','Monte Vista Drive','Monterey Street','Monticello Court','Morgan Court','Moriarty Street','Morisson Drive','Morning Dove Lane','Morningside Lane','Morrison Drive','Mountain View Avenue','Mozumdar Drive','Mulvihill Avenue','Myra Street','Myrtle Street','N 1st Street','N 5th Street','N 6th Street','N Ash Street','N Buena Vista Street','N Carolyn Court','N Center Place','N Center Street','N Dearborn Street','N Denise Avenue','N Eureka Street','N Grove Street','N Jeremy Court','N Kendall Street','N la Salle Street','N Lincoln Street','N Michigan Street','N New York Street','N Poppy Road','N Rose Arbor Court','N San Mateo Street','N University Street','N Wabash Avenue','Nanette Street','Naomi Street','Napa Avenue','Naples Avenue','Naranjo Court','Nathan Court','Nelson Street','Nevada Street','New Jersey Street','New York Street','Nice Avenue','Nickolas Avenue','Nordina Street','Normandie Court','North Place','Northview Place','Norwood Street','Nottingham Drive','Oak Grove Drive','Oak Street','Oak Wood Circle','Occidental Circle','Occidental Drive','Ohio Street','Olive Avenue','Opal Avenue','Orange Avenue','Orange Park','Orange Street','Orange Tree Lane','Orchard Drive','Orchid Court','Oriental Avenue','Outer Highway 10 S','Overcrest Drive','Oxford Drive','Pacific Street','Padua Avenue','Paige Lane','Paiute Avenue','Pala Bells Court','Palmbrook Drive','Palmetto Avenue','Palo Alto Court','Palo Alto Drive','Palo Verde Drive','Paloma Avenue','Palomares Road','Pamela Crst','Panorama Drive','Paradise Way','Parker Court','Parkford Drive','Parkview','Parkwood Drive','Patricia Drive','Pecos Street','Pedley Street','Pennsylvania Avenue','Pepper Way','Phelan Avenue','Phlox Avenue','Phlox Court','Piedmont Lane','Pilgrim Road','Pine Avenue','Pine Knoll Cres','Pinewood Court','Pinon Road','Pioneer Avenue','Placer Street','Pleasantview Drive','Plum Lane','Ponderosa Road','Poppy Road','Post Street','Powell Lane','Prado Lane','Prado Street','Price Street','Primrose Avenue','Priscilla Way','Prospect Court','Prospect Drive','Providence Place','Pueblo Avenue','Puesta del Sol','Puesta del Sol Street','Pummelo Drive','Purdue Avenue','Puritan Place','Quail Court','Quincy Court','Rachel Court','Raemee Avenue','Rainbow Lane','Rainier Court','Ramona Drive','Rancho Drive','Rebecca Crst','Red Bird Court','Redlands Boulevard','Redlands Street','Reed Street','Rees Court','Refuse Road','Renee Street','Research Drive','Reservoir Canal Road','Reservoir Road','Revelation Way','Rhonda Lane','Rhondda Street','Ridge Street','Ridgeview Court','Riley Way','River Bend Drive','Riverview Drive','Roberts Road','Robinhood Lane','Robyn Street','Rolling Hills Road','Roma Street','Romero Road','Roosevelt Road','Rosalie Court','Rose Street','Rosehill Crst','Rossmont Drive','Ruby Avenue','Ruiz Street','Ryan Street','S 4th Street','S 5th Street','S 6th Street','S Ash Street','S Belair Court','S Buena Vista Street','S Center Street','S Church Street','S Cll de Las Palmas','S Cll Ocotillo','S Dearborn Street','S Eureka Court','S Eureka Street','S Grove Street','S la Salle Street','S Lincoln Street','S Michigan Street','S Nanette Street','S San Mateo Street','S Serpentine Drive','S Shadowbrook Court','S University Street','S Valle del Sol Drive','S Wabash Avenue','Sage Court','Sage Road','Saint Catherine Street','Salem Drive','San Bernardino Avenue','San Bernardino Fwy','San Gorgonio Drive','San Jacinto Street','San Juan Avenue','San Marcos Avenue','San Mateo','San Pablo Avenue','San Rafael Street','San Timoteo Acrd','San Timoteo Canyon Road','Sand Canyon Road','Sand Hill Road','Sandalwood Avenue','Sandra Way','Sandy Court','Sarrita Drive','Saugus Court','Scenic Terrace','Scott Canyon Acrd','Serpentine Drive','Sespe Court','Sessums Drive','Severn Street','Shawn Court','Sheffield Lane','Sherril Lane','Sherry Way','Sherwood Street','Shirley Lane','Sierra Crest Court','Sierra Vista Drive','Silver Cup Court','Silverleaf Court','Silvertree Lane','Silverwood Place','Sinclair Court','Smiley Boulevard','Smiley Heights Drive','Smiley Ridge','Smiley Road','Snowden Avenue','Solano Way','Somerset Lane','Sonata Drive','Sonora Circle','Sonora Street','Sophia Court','South Lane','Sparrow Court','Standish Way','Star Ruby Court','Starlight Court','State Route 38','State Route 210','Steele Street','Sterling Avenue','Sterling Drive','Sterling Road','Stickney Circle','Stillman Avenue','Stony Court','Strada Casalingo','Stratford Circle','Sue Avenue','Summit Avenue','Summit B Avenue','Sundown Court','Sunflower Street','Sunnypark','Sunnyside Avenue','Sunridge Way','Sunset Ct N','Sunset Hills Lane','Sunset Lane','Susan Avenue','Sutherland Drive','Sylvan Boulevard','Taff Street','Tamarisk Street','Tanforan Way','Tangerine Drive','Tennessee Street','Terracina Boulevard','Texas Street','Thames Street','The Terrace','Thomas Avenue','Thomas Road','Tivoli Drive','Torino Street','Tri City Center','Tribune Street','Tudor Court','Tulane Court','University Place','Vache Circle','Valencia Drive','Valencia Lane','Valle del Sol','Valle Vista Drive','Valley Falls Avenue','Valley View Drive','Valley View Lane','Vally Falls Avenue','Van Ness Lane','Velwood Drive','Venice Cove Court','Verde Vista Drive','Verlie Drive','Vermont Street','Verona Drive','Via Antibes','Via Barcelona','Via del Sol','Via Florence','Via Nice','Via Palermo','Via Ravenna','Via San Remo','Via Vista Drive','Village Street','Vinton Way','Violet Street','Virginia Street','W Brockton Avenue','W Citrus Avenue','W Clark Street','W Clifton Avenue','W Colton Avenue','W Crescent Avenue','W Cypress Avenue','W Delaware Avenue','W Domestic Avenue','W Fern Avenue','W High Avenue','W Highland Avenue','W Hilton Avenue','W Home Place','W Lugonia Avenue','W Mariposa Drive','W Mill Street','W Mountain View Circle','W Mountain View Street','W Olive Avenue','W Palm Avenue','W Palm Lane Drive','W Park Avenue','W Pearl Avenue','W Pennsylvania Avenue','W Pilgrim Road','W Pioneer Avenue','W Redlands Boulevard','W San Bernardino Avenue','W Serpentine Drive','W Sharon Road','W South Avenue','W State Street','W Stuart Avenue','W Sun Avenue','W Sunser Drive','W Sunset Drive','W Sunset Drive S','W Union Avenue','W Vine Street','W Western Avenue','Wabash Avenue','Walnut Avenue','Walnut Street','Washington Street','Waterford Avenue','Waters Court','Webster Street','Westbrook Circle','Westpark','Westwood Lane','Whittier Avenue','Wilbar Circle','Willowcreek Drive','Wimbleton Drive','Woodbury Street','Wooden Bridge Lane','Yucaipa Ridge Truck Trail','Yukon Street','Yvette Court'];
  
  
  public allCorners = [["madeup",  "test"] , ["wrong", "answer"], ["W Fern Avenue", "S Center Street"], ["Chestnut Avenue", "Ramona Drive"], ["more", "needed"], ["W Palm Avenue", "S Buena Vista Street"] , ["W Clark Street", "S Michigan Street"], [ "San Jacinto Street", "Walnut Avenue"] , ["Lakeside Avenue", "Friar Lane"], ["La Loma Drive", "La Feliz Drive"], ["Edgemont Drive", "Fairmont Drive"], ["Franklin Avenue", "E South Avenue"], ["Monterey Street", "W Palm Avenue"], ["Glenwood Drive", "S Buena Vista Street"],["W Olive Avenue", "Alvarado Street"], ["W Home Place", "S 4th Street"], ["Judson Street", "Clock Avenue"], ["E Clark Street", "Myrtle Street"], ["Occidental Drive", "Campus Avenue"], ["E Brockton Avenue", "Herald Street"], ["W Fern Avenue", "Sherwood Street"], ["S Center Street", "Chestnut Avenue"], ["Walnut Avenue", "Pacific Street"], ["W Cypress Avenue", "Harding Drive"], ["S San Mateo Street", "Magnolia Avenue"], ["Lakeside Avenue", "Mills Avenue"], ["Brookside Avenue", "Brookdale Drive"], ["Dreka Avenue", "Clay Street"], ["Ruby Avenue", "Columbia Street"] ,["6th Street", "E Western Avenue"], ["Nottingham Drive", "Friar Lane"]] ;
  public allHouse = [1,2,3,4,5,6];

  public gameWon = false;
  public yesDisplay = true;
  public congratsMSG = [["Amazing", "Brilliant", "Perfect", "Astounding", "Ingenius"], ["Congrats", "Great Playing", "Superb", "Too Easy"], ["Not Bad", "Good Game", "Not to shabby", "Well Done"], ["Acceptable", "Not the worst", "Could be better", "Mediocre"], ["Phew", "Just Barely", "Alright", "Last Try"]];
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

  //fifth guess
  public selectedStreet9 = '';
  public selectedStreet10 = '';
  public guess5Selected = false;
  public bgcolor9 = "white";
  public bgcolor10 = "white";
  public disabled9 = false;
  public disabled10 = false;

  public guessCount = 0;
  
  //date functions-------------------------------------------------------------------------------------------------------------------
  getDate() {
    return new Date();
  }
  getDayOfYear(date: Date) {
    let start = new Date(date.getFullYear(), 0, 0);
    let diff = date.getTime() - start.getTime() + (start.getTimezoneOffset() - date.getTimezoneOffset()) * 60 * 1000;
    let day = Math.floor(diff / 86400000) % 29;
    return day + 1;
  }

  public x =  this.getDayOfYear(this.getDate()); 

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


   //for guess 4 ------------------------------------------------------------------------------------------------------------

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

  //for guess 5 ------------------------------------------------------------------------------------------------------------

  checkStreet9(k: any, j: any): boolean{
    if (j.includes(k)){
      this.bgcolor9 = "#80ff80";
      return true;
    }
    else{
      this.bgcolor9 = "#ff8080";
      return false;
    }
  }

  checkStreet10(k: any, j: any): boolean{
    if (j.includes(k)){
      this.bgcolor10 = "#80ff80";
      return true;
    }
    else{
      this.bgcolor10 = "#ff8080";
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
        localStorage.guess5Selected = false;
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

        localStorage.guess5street1 = null;
        localStorage.guess5street2 = null;
        localStorage.street9 = '';
        localStorage.street10 = '';
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

    //for guess 5
    if (localStorage.street9) {
      this.selectedStreet9 = localStorage.street9;
    }
    if (localStorage.street10) {
      this.selectedStreet10 = localStorage.street10;
    }
   
    if (localStorage.guess5Selected != null) {
      this.guess5Selected = localStorage.guess5Selected === "true";
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

    // guess 5
    if (localStorage.guess5street1 === "true") {
      this.bgcolor9 = "#80ff80";
    } else if (localStorage.guess5street1 === "false") {
      this.bgcolor9 = "#ff8080";
    } else {
      this.bgcolor9 = "white";
    }
    if (localStorage.guess5street2 === "true") {
      this.bgcolor10 = "#80ff80";
    } else if (localStorage.guess5street2 === "false") {
      this.bgcolor10 = "#ff8080";
    } else {
      this.bgcolor10 = "white";
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
        this.guess5Selected = true;
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
      this.guess5Selected = true;
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
      this.guess5Selected = true;
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
      this.guess5Selected = true;
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


 setFifthGuess(street9: string, street10: string) {
   
  if (street9 != street10 && street9 != "" && street10 != "" && this.allStreets.includes(street9) && this.allStreets.includes(street10)){
  let s1 = this.checkStreet9(street9, this.allCorners[this.x]);
  let s2 = this.checkStreet10(street10, this.allCorners[this.x]);
  localStorage.guess5street1 = s1;
  localStorage.guess5street2 = s2;
   if (!this.guess5Selected){
      this.guessCount += 1;
      // this.totalGuesses += 1;
    }
   if (s1 && s2){
      this.gameWon = true;
      if (!this.guess5Selected){
        this.totalStars += 1;
      }
    }
   localStorage.street9 = street9;
   localStorage.street10 = street10;
   this.guess5Selected = true;
   this.disabled9 = false;
   this.disabled10 = false;
   }
   else {
      if (street9 == "" || !this.allStreets.includes(street9)) {
        this.disabled9 = true;
      }
      if (street10 == "" || !this.allStreets.includes(street10)) {
        this.disabled10 = true;
      }
      if (street9 == street10) {
        this.disabled9 = true;
        this.disabled10 = true;
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
  left: 50%;
  margin-right: -50%;
  transform: translate(-50%, -10%);
  

  font-size: 30px;
  font-family: nunito,roboto,proxima-nova,"blippo", fantasy;
  background-color: rgb(241, 252, 241);
  color: #fa9a4c;
  border-radius: 20px;
  width: 500px;
  height: 500px;
  border: 0px solid #a09f9f;
  box-shadow: 0 0 0.9em rgb(161, 253, 143);

  top: 30%;
  
}
.loss{
  z-index: 4;
  position: absolute;
  left: 50%;
  margin-right: -50%;
  transform: translate(-50%, -10%);
  font-size: 30px;
  font-family: nunito,roboto,proxima-nova,"blippo", fantasy;
  background-color: rgb(241, 252, 241);
  color: #fa9a4c;
  top: 30%;
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
  
  cursor: pointer;
  display: inline-block;
  font-family: nunito,roboto,proxima-nova,"proxima nova",sans-serif;
  font-size: 80%;
  font-weight: 1000;
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
  width: 15dvw;
  
  
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
.and{
  font-family: nunito,roboto,proxima-nova,"proxima nova",sans-serif ;
  font-weight: bold;
  color: white;
  background-color: #2185f8;
  border-radius: 15%;
}
</style>
<!-- #80ff80 -->
<!-- #ff8080 -->