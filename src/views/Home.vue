<!-- Home.vue and dispatcher.vue sends and recives messages to/from the server.
     v-bind binder något till ett namn?
    cd /Users/simonolausson/Documents/Gränssnittsproggramering/1md031-lab-21
    npm run serve

-->

<template> <!-- HTML -->

  <div id="mapWrapper">
    <div id="map" v-on:klick="addOrder">
      click here
    </div>
  </div>

  <header id="head">
    <img src="https://www.mcdonalds.com/is/image/content/dam/se/nfl/Core/Footer/OmOss/mcd-sv-core-om-oss2-desktop.jpg?$Hero_Desktop$">
    <h1> Välkommen till burgeronline</h1>
  </header>

  <div class="wrapper"> <!-- Denna div är en component som itererar över alla burgare i burgers -->
    <Burger v-for="burger in burgers"
            v-bind:burger="burger"
            v-bind:key="burger.name"
            v-on:orderedBurger="addToOrder($event)"
    />
  </div>
  <main>
    <!--
    <section id="hamburgare">
      <h2> Hamburgare</h2>
      <p>Här väljer du vilken hamburgare du vill ha</p>
      <div class="wrapper">
        <div class="box a">
          <h2> Amerikansk</h2>
          <img src="https://img.koket.se/standard-mega/klassisk-amerikansk-hamburgare.jpg.webp" alt="Span" title="Another in-line element" style="width: 200px;">
          <section class="ingredienser">
            <ul>
              <li>Innehåller kött</li>
              <li>Innehåller gluten</li>
              <li>Innehålle laktos</li>
              <li>väldigt god</li>
            </ul>
          </section>
        </div>
        <div class="box b">
          <h2> smashad</h2>
          <img src="https://files.allas.se/uploads/sites/25/2020/12/smashade-burgare-godaste-hemgjorda-hamburgaren-1024x683.jpg" alt="Span" title="Another in-line element" style="width: 200px;">
          <section class="ingredienser">
            <ul>
              <li>Innehåller kött</li>
              <li>Innehåller gluten</li>
              <li>Innehålle laktos</li>
              <li>väldigt god</li>
            </ul>
          </section>
        </div>
        <div class="box c">
          <h2> Maxad</h2>
          <img src="https://www.max.se/contentassets/1fdf0ed6657c4de8a5a89751b81bb875/product_hamburgare.png?width=1160&sharpen=5&sigma=1,4&threshold=0" alt="Span" title="Another in-line element" style="width: 200px;">
          <section class="ingredienser">
            <ul>
              <li>Innehåller kött</li>
              <li>Innehåller gluten</li>
              <li>Innehålle laktos</li>
              <li>väldigt god</li>
            </ul>
          </section>
        </div>
      </div>

    </section>
    -->
    <section id="kundinfo" style="clear:left">
      <h2>Information  om kund</h2>
      <p>Här kan du ange information om dig själv såsom leveransadress osv.</p>
      <h3>Information om leverans</h3>
      <p>
        <label for="namn">Namn</label><br>
        <input type="text" id="namn" v-model="namn" required="required" placeholder="För och efternamn">
        {{namn}}
      </p>
      <p>
        <label for="email">Email</label><br>
        <input type="email" id="email" v-model="email" required="required" placeholder="E-mail address">
        {{email}}
      </p>
      <p>
        <label for="gata">Gata</label><br>
        <input type="text" id="gata" v-model="gata" required="required" placeholder="Namn på gata">
        {{gata}}
      </p>
      <p>
        <label for="husnummer">Hus</label><br>
        <input type="text" id="husnummer" v-model="husnummer" required="required" placeholder="husnummer">
        {{husnummer}}
      </p>
      <p>
        <label for="Betalsätt">Betalsätt </label>
        <select id="Betalsätt" v-model="betalsätt" >
          <option>Kort</option>
          <option>Paypal</option>
          <option selected="selected">Swish</option>
          <option>Bitcoin</option>
        </select>
        {{betalsätt}}

      </p>
      <p>Kön :{{kön}}</p>
      <div>
        <input type="radio" id="Man" v-model="kön" value="Man">
        <label for="Man">Man</label>
      </div>
      <div>
        <input type="radio" id="Kvinna" v-model="kön" value="Kvinna">
        <label for="Kvinna">Kvinna</label>
      </div>
      <div>
        <input type="radio" id="Vill ej uppge" v-model="kön" value="Vill ej uppge" checked="checked">
        <label for="Vill ej uppge">Vill ej uppge</label>
      </div>
    </section>
    <button type="submit" v-on:click="handleClick">
      <img src="https://educaora.com/api/editors/6176786d68d9913b4bb2739c/published-files/image_button.png">
    </button>
    <footer>
      <hr>
      <p>Copyright</p>
    </footer>
  </main>

</template>

<script> //JAVASCRIPT
import Burger from '../components/Burger.vue'
import io from 'socket.io-client'
import menu from '../assets/menu.JSON'

const socket = io();

//HÄR SKA JAG SKRIVA KODEN
 const burgers = menu;

// function Menuitem (name, image, kCal, gluten, lactose){
//   this.name = name
//   this.image = image
//   this.kCal = kCal
//   this.gluten = gluten
//   this.lactose = lactose
// }
//
// const burgers = [
//     new Menuitem("burger","https://img.koket.se/standard-mega/klassisk-amerikansk-hamburgare.jpg.webp","123",true, false),
//     new Menuitem("berger","https://files.allas.se/uploads/sites/25/2020/12/smashade-burgare-godaste-hemgjorda-hamburgaren-1024x683.jpg","1000",false,false),
//     new Menuitem("birger","https://www.max.se/contentassets/1fdf0ed6657c4de8a5a89751b81bb875/product_hamburgare.png?width=1160&sharpen=5&sigma=1,4&threshold=0","999",true,true)
// ]


console.log(burgers)

export default {                                       
  name: 'Home',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers:burgers,
      namn:"",
      email:"",
      gata:"",
      husnummer:"",
      kön:"Vill ej uppge",
      betalsätt:""
    }
  },
  methods: { // JS-metoder, kan vara rätt viktig i labben.
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    addOrder: function (event) {
      let offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};

      socket.emit("addOrder", { orderId: this.getOrderNumber(), //socket.emit is sending a message. Socket.on is a listener.
                                details: { x: event.clientX - 10 - offset.x,
                                           y: event.clientY - 10 - offset.y },
                                orderItems: ["Beans", "Curry"]
                              }
                 );
    },
    handleClick: function() {
      console.log(this.namn, this.email, this.gata, this.husnummer, this.kön, this.betalsätt)
    },
    addToOrder: function (event) {
      console.log(event.name, event.amount)
      //this.orderedBurger[event.name] = event.amount; //DET ÄR HÄR DEN SLUTAR FUNKA
    },
  }
}
</script>

<style>
@import 'https://fonts.googleapis.com/css?family=Pacifico|Dosis';

  #map {
    width: 1920px;
    height: 1078px;
    background: url("/img/polacks.jpg");
  }
  #mapWrapper{
  width: 1000px;
  height: 500px;
    overflow: scroll;

  }

  body {
    font-family: arial;
    color:black;
    font-size: 1.3em;
  }

  .ingredienser {
    color: #ff5500;
    font-weight: bold;
  }

  .wrapper {
    display: grid;
    grid-gap: 10px;
    padding: 10px;
    /*grid-template-columns: 400px 400px 400px;*/
    grid-template-columns: auto auto auto;
    background-color: #fff;
    color: #444;
    border-style: dashed;
  }

  .box {
    border-style: dashed;
    /*background-color: #444;*/
    color: #fff;
    border-radius: 5px;
    padding: 10px;
    font-size: 100%;
  }

  .a {
    grid-column: 1;
  }
  .b {
    grid-column: 2 ;
  }
  .c {
    grid-column: 3 ;

  }

  #kundinfo {
    background-color: black;
    color:white;
    border-style: dashed;
    padding-left: 10px;
    padding-bottom: 10px;
  }

  section{
    margin-left: 10px;
  }
  #hamburgare {
    border-style: dashed;
    padding: 10px;
  }

  #hamburgare div{    /*betyder alla divs som är barn till id't hamburgare*/
    padding:20px;
  }

  button:hover {
    background-color:lawngreen;
    cursor: pointer;
  }

  button{
    margin:20px;
  }

  #head{
    margin-left:10px;
    height: 200px;
    width: 100%;
    overflow: hidden;
    padding-left: 100px;
    padding-right: 100px;
  }
  #head img{
    opacity: 50%;
  }
  #head h1{
    position: absolute;
    margin-top: -500px;
  }



</style>
