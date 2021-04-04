<template>
  <div class="hello">
    <div class="container d-flex justify-content-center">
      <img src="@/assets/starwars.png" alt="">
    </div>
    <div class="container">
    </div>
    <div class="container">
      <div class="row">
        <div v-for="result in results" v-bind:key="result" class="col">
          <div class="card mb-3 border-0 shadow" style="width: 20rem;">
            <div class="card-body">
              <h5 class="card-title">{{ result.name }}</h5>
              <p class="card-text">Lorem ipsum dolor sit amet consectetur, adipisicing elit. Minus, ipsa.</p>
              <ul class="list-group list-group-flush">
                <li class="list-group-item">birth year: {{ result.birth_year }} </li>
                <li class="list-group-item">gender: {{ result.gender }}</li>
                <li class="list-group-item">homeworld: {{ result.planet.name }} </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data() {
      return {
        results: [],
      }
    },
    props: {
      msg: String,
    },
    methods: {
      getStarwars() {
        axios.get('https://swapi.dev/api/people/')
          .then(response => this.results = response.data.results).then(response => {
            for (let i = 0; i < 10; i++) {
              axios.get(response[i].homeworld).then(result => {
                this.results[i].planet = (result.data);
              })
            }
          });
      }
    },

    created() {
      this.getStarwars()
    }
  }
</script>