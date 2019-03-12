<template>
  <div style="padding: 30px;">
    <h1>Final Assignment</h1>

    <h3>1. Display a message</h3>
    <!-- display 'message' here -->

    <br />Message: <b>{{ message }}</b> <br /><br />

    <h3>2. Add 2 properties</h3>
    <!-- diplsay the sum of value1 and value2 -->
    <br />
    Sum of Values: <b>{{ value1 + value2 }}</b> <br /><br />

    <h3>3. Display a list</h3>
    <!-- display a list from the myList array in data -->
    <ul v-for="list in myList">
      <li>{{ list }}</li>
    </ul>

    <h3>4. Display a list of lists</h3>
    <!-- display a list of lists from the categorizedList array in data -->
    <ul>
      <li v-for="list in categorizedList">
        {{ list.name }}
        <ul v-for="item in list.items">
          <li>{{ item }}</li>
        </ul>
      </li>
    </ul>

    <h3>5. Display an HTML card using data</h3>
    <!-- use vacationCardData to fill in the below card -->
    <div class="card">
      <div class="card-image">
        <img v-bind:src="vacationCardData.imgSrc" class="img-responsive" />
      </div>
      <div class="card-header">
        <div class="card-title h5">{{ vacationCardData.title }}</div>
        <div class="card-subtitle text-gray">
          {{ vacationCardData.subtitle }}
        </div>
      </div>
      <div class="card-body">{{ vacationCardData.description }}</div>
    </div>

    <h3>6. Display a Card Component</h3>

    <gbc-card v-bind="vehichleCardData"></gbc-card>

    <h3>7. Display a Card by making a call</h3>
    <!--
      Call and load vehicle-detail.json using axios and display the data in an html card
    -->
    <div class="card">
      <div class="card-image">
        <img v-bind:src="vehicleDetail.imgSrc" class="img-responsive" />
      </div>
      <div class="card-header">
        <div class="card-title h5">{{ vehicleDetail.title }}</div>
        <div class="card-subtitle text-gray">{{ vehicleDetail.subtitle }}</div>
      </div>
      <div class="card-body">{{ vehicleDetail.description }}</div>
    </div>

    <h3>8. Display a Card Copmonent by making a call</h3>
    <!--
      Call and load vehicle-detail.json using axios and display the data in a card component
    -->
    <!-- <gbc-card></gbc-card> -->
    <gbc-card
      v-bind:title="vehicleDetail.title"
      v-bind:subtitle="vehicleDetail.subtitle"
      v-bind:description="vehicleDetail.description"
      v-bind:imgSrc="vehicleDetail.imgSrc"
    ></gbc-card>

    <h3>9. Display a list of cards using data from vehicles-list.json</h3>
    <div class="container">
      <div class="columns">
        <div class="column col-4" v-for="vehicles in vehiclesList">
          <gbc-card
            v-bind:title="vehicles.title"
            v-bind:subtitle="vehicles.subtitle"
            v-bind:description="vehicles.description"
            v-bind:imgSrc="vehicles.imgSrc"
          ></gbc-card>
        </div>
      </div>
    </div>

    <h3>10. Display some of Bublbasaur's information from the pokeapi</h3>
    <ul>
      <li>
        Pokemon Name: <b> {{ bublbasaursInfo[0].name }}</b>
      </li>
      <li>
        Base Experience: <b> {{ bublbasaursInfo[0].base_experience }}</b>
      </li>
      <li>
        Weight: <b> {{ bublbasaursInfo[0].weight }}</b>
      </li>
      <li>
        height: <b> {{ bublbasaursInfo[0].height }}</b>
      </li>
    </ul>

    <h3>11. Display Bulbasaur's abilities in a list from the pokeapi</h3>
    <ul v-for="Ability in bublbasaursAbilities">
      <li>
        Ability : <b>{{ Ability.ability }}</b>
      </li>
    </ul>

    <h3>12. Display Bublbasaur's stats in a list from the pokeapi</h3>
    <ul v-for="stat in bublbasaurstats">
      <li>
        Stat name : <b>{{ stat.stats }}</b> --- Base_stat :
        <b>{{ stat.base_stat }}</b>
      </li>
    </ul>

    <h3>13. Display Bublbasaur's first 5 moves in a list from the pokeapi</h3>
    Bublbasaur's first 5 Moves
    <ul v-for="pokemon in bublbasaurPokemonMoves">
      <li>
        <b> {{ pokemon.move }}</b>
      </li>
    </ul>

    <h3>
      14. Display Bublbasaur's first 5 moves with power and accuracy in a list
      from the pokeapi
    </h3>
    Bublbasaur's first 5 Moves with power and accuracy
    <ul v-for="pokemon in bublbasaurPokemonMoves">
      <li>
        <b> {{ "Move :  " + pokemon.move }}</b> -
        {{ "power :  " + pokemon.power }} -
        {{ "Accuracy :  " + pokemon.accuracy }}
      </li>
    </ul>

    <h3>
      Display the first 15 pokemon and their first 3 moves (name, power,
      accuracy)
    </h3>
    <ul v-for="pokemon in firstFiftenPokemon">
      <b>{{ "Pokemon:  " + pokemon.movename }}</b>

      <li
        v-for="moves in firstFiftenPokemonMoves"
        v-if="pokemon.movename === moves.movename"
        id="visible"
      >
        {{ "Move :  " + moves.move }}

        <ul id="hidden" v-if="moves.accuracy !== null">
          <b>
            {{ " Accuracy:  " + moves.accuracy }} -
            {{ " Power:  " + moves.power }}</b
          >
        </ul>
        <ul id="hidden" v-else>
          <b> {{ " Moves with no accuracy and power  " }} </b>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import GbcCard from "./components/card";
export default {
  name: "App",
  components: {
    GbcCard
  },
  data() {
    return {
      message: "Hello World",
      value1: 1337,
      value2: 42,
      myList: ["Xbox", "Playstation", "Nintendo Switch", "Sega"],
      categorizedList: [
        {
          name: "Category 1",
          items: ["item 1", "item 2", "item 3"]
        },
        {
          name: "Category 2",
          items: ["item a", "item v", "item c"]
        },
        {
          name: "Category 3",
          items: ["item i", "item ii", "item iii"]
        }
      ],
      vehicleDetail: [],
      vehiclesList: [],
      firstFiftenPokemon: [],
      firstFiftenPokemonMoves: [],
      bublbasaurPokemonMoves: [],
      bublbasaurstats: [],
      bublbasaursAbilities: [],
      bublbasaursInfo: [],
      vacationCardData: {
        title: "My Favorite Vacation",
        subtitle: "Anywhere warmer than here",
        description:
          "Cancún, a Mexican city on the Caribbean Sea, is known for its beaches",
        imgSrc:
          "https://media.triseptsolutions.com/sites/VAXWEBWNT/PublishingImages/Themes/Destinations/Aruba_Beach_382x235.jpg"
      },
      vehichleCardData: {
        title: "Toyota Corolla",
        subtitle: "Midsize Sedan",
        description: "Great car that gets you from point a to point b",
        imgSrc:
          "https://postmediadriving.files.wordpress.com/2017/11/chrome-image-395391.png?w=800&h=520&crop=1"
      }
    };
  },
  mounted() {
    axios.get("/vehicles-list.json").then(response => {
      this.vehiclesList = response.data.vehicles;
    });

    axios.get("/vehicle-detail.json").then(response => {
      this.vehicleDetail = response.data.vehicleDetail;
    });

    //Question 15.
    axios.get("https://pokeapi.co/api/v2/pokemon/").then(response => {
      // loop through abilities and make requests to get additiona ability data

      response.data.results.slice(0, 15).forEach(moveName => {
        // use 'url in 'ability.ability' object as paramter for axios.get
        this.firstFiftenPokemon.push({
          movename: moveName.name
        });
        axios.get(moveName.url).then(response => {
          let ability = response.data;
          // add data from response to our array

          ability.moves.slice(0, 3).forEach(move => {
            axios.get(move.move.url).then(moveResponse => {
              let moveAccuracy = moveResponse.data;

              this.firstFiftenPokemonMoves.push({
                movename: moveName.name,
                move: move.move.name,
                accuracy: moveAccuracy.accuracy,
                power: moveAccuracy.power
              });
            });
          });
        });
      });
    });

    //Question 14
    axios.get("https://pokeapi.co/api/v2/pokemon/1/").then(response => {
      let ability = response.data;

      ability.moves.slice(0, 5).forEach(move => {
        // ex.(move.url) is https://pokeapi.co/api/v2/move/razor-wind
        axios.get(move.move.url).then(moveResponse => {
          let moveAccuracy = moveResponse.data;
          this.bublbasaurPokemonMoves.push({
            move: move.move.name,
            accuracy: moveAccuracy.accuracy,
            power: moveAccuracy.power
          });
        });
      });
    });

    axios.get("https://pokeapi.co/api/v2/pokemon/1/").then(response => {
      let ability = response.data;
      ability.stats.forEach(basestats => {
        this.bublbasaurstats.push({
          stats: basestats.stat.name,
          base_stat: basestats.base_stat
        });
      });
    });

    axios.get("https://pokeapi.co/api/v2/pokemon/1/").then(response => {
      let ability = response.data;
      ability.abilities.forEach(response => {
        this.bublbasaursAbilities.push({
          ability: response.ability
        });
      });
    });

    axios.get("https://pokeapi.co/api/v2/pokemon/1/").then(response => {
      let info = response.data;

      this.bublbasaursInfo.push({
        base_experience: info.base_experience,
        name: info.name,
        weight: info.weight,
        height: info.height
      });
      console.log(this.bublbasaursInfo);
    });
    // 1. Display the message in data
    // 2. Display the sum of value1 and value 2 in data
    // 3. Display a list from the myList array in data
    // 4. Display a list of lists from the categorizedList array in data
    // 5. Display data from vacationCardData inside the card html provided
    // 6. Build and display a card component by passing vehichleCardData as props to card
    // make sure to create the card component file in components and import it
    // 7. Call and load vehicle-detail.json using axios and display the data in an html card
    // 8. Call and load vehicle-detail.json using axios and display the data in a card component
    // 9. Display a list of cards using data from vehicles-list.json
    // 10. Display some of Bublbasaur's information from the pokeapi
    // get url https://pokeapi.co/api/v2/pokemon/bulbasaur/
    // documentation for the pokeapi can be found: https://pokeapi.co/docs/v2.html/
    // 11. Display Bublbasaur's abilities in a list from the pokeapi
    // 12. Display Bublbasaur's stats in a list from the pokeapi
    // 13. Display Bublbasaur's first 5 movies in a list from the pokeapi
    // 14. Display Bublbasaur's first 5 moves with power and accuracy in a list from the pokeapi
    //   you will have to use https://pokeapi.co/api/v2/move/{name} api to get move details
    //   like power and accuracy, pass the move name to the call, ex:
    //   https://pokeapi.co/api/v2/move/razor-wind
    // 15: BONUS.
    //   a. Display a list of names of the first 15 pokemon from the pokeapi.co api (https://pokeapi.co/api/v2/pokemon/)
    //   b. For each pokeon name in the list, list below their first 3 move name
    //   c. When hovering over each move name display the move accuracy and power
  },
  methods: {}
};
</script>
<style>
#hidden {
  display: none;
}
#visible:hover #hidden {
  display: block;
}
</style>
