<template>
    <header>
      <h1>Countries API</h1>
    </header>
    <section class="countries">
      <div class="countries-wrapper" v-for="(countries, idx) in countriesName" :key="idx">
        <div class="card">
          <img :src="countries.flag">
          <div class="card-body">
            <h2>{{ countries.name }}</h2>
            <p>IS0: {{ countries.iso2 }}</p>
          </div>
        </div>
      </div>
    </section>
</template>

<script>
import { toRefs, reactive } from "vue";

export default {
  name: 'App',

  setup() {
    const state = reactive({
      countriesName: {},
      countries: "",
    });

    console.log(state.countries);

    fetch("https://countriesnow.space/api/v0.1/countries/flag/images")
    .then(response => response.json())
    .then(data => {
      //console.log(data.data[1].flag);
      state.countriesName = data.data;
    })

    return {
      ...toRefs(state),
    }
  }

}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
}

header {
  text-align: center;
  font-size: 4vmin;
}

.countries {
    min-height: 70vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
}

.card{
    width: 300px;
    height: 189px;
    cursor: pointer;
    border-radius: 16px;
    box-shadow: 0 0 13px 0px rgba(0,0,0,.3);
    transition: .5s;
    overflow: hidden;
    margin: .85rem;
}

.card:hover{
    height: 280px;
}

.card img{
    width: 302px;
    height: 189px;
    border-radius: 16px;
    transition: .5s;
}

.card:hover img{
    border-radius: 16px 16px 0 0;
}

.card .card-body{
    padding: .5rem .85rem 1rem;
    height: 0;
}

.card .card-body h2{
    margin: .5rem 0;
    font-size: .85rem;
    color: hsl(240, 27%, 39%);
    letter-spacing: 3px;
}

.card .card-body p{
    text-align: justify;
    font-size: .9rem;
    line-height: 25px;
}


</style>
