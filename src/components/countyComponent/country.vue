<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { onMounted, ref } from 'vue'

let id = ref(0)

let Allcountries = ref({})
const url = 'https://restcountries.com/v3.1/all'
// function fetchCountry() {
//   try {
//     Allcountries.value = fetch(url)
//       .then((res) => res.json())
//       .then((data) => console.log(data))
//   } catch (error) {
//     console.error(error)
//   }
// }
async function fetchCountry() {
    const resp = await fetch(url)
    Allcountries.value = await resp.json()
    console.log(Allcountries.value);
    
}

onMounted(()=>{
    fetchCountry()
})


</script>
<template>
  <header>
    <h1 class="">{{ Allcountries[id]?.name.official }}</h1>
  </header>
  <main>
    <section>
      <article>
        <img :src= "Allcountries[id]?.flags.png"  alt=""  class="drapeau"/>
        <div class="liste">
          <h4>Liste des pays</h4>
          <ul>
            <li @click="(()=>id=index)" v-for="(country,index) in Allcountries" :key="index" ><a href="#">{{ country.name.official }}</a></li>
          </ul>
        </div>
      </article>
      <article class="infos">
        <article>
          <div class="prio">
            <p><span> Capital:</span>{{ Allcountries[id]?.capital[0] }}</p>
            <p><span> Monnaie:</span>{{Object.values(Allcountries[id]?.currencies)[0].name}}</p>
            <p><span> Langue:</span>{{Object.values(Allcountries[id]?.languages)[0]}}</p>
            <p><span> Sous-région:</span>{{Allcountries[id]?.subregion}}</p>
            <p><span> Emblème:</span><img :src="Allcountries[id]?.coatOfArms.png" alt="" style="width: 100px; height: 100px;"></p>
          </div>
          <div class="autres">
            <p>Autres infos</p>
            <p><span> Population:</span>{{ Allcountries[id]?.population}}</p>
          </div>
        </article>



        <div class="propos">
          <h3>A propos</h3>
          <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Possimus minima incidunt
            exercitationem officia minus recusandae ullam saepe, cumque ut culpa dolorem quia
            aliquid quas voluptatum. Similique nemo repudiandae modi corrupti explicabo velit,
            praesentium, aliquam at eos commodi inventore esse adipisci necessitatibus facere quos
            error incidunt culpa doloremque rem tenetur porro natus officiis saepe. Quos cupiditate
            cumque, quis neque quae quaerat numquam molestiae fugit, minima quasi quia facere,
            similique nostrum? Optio ullam commodi voluptatibus similique amet deserunt impedit
            delectus. Illum quo iusto iste vitae, et praesentium aut provident! Reprehenderit
            incidunt laborum dolor velit quis rem itaque quidem id illum voluptates porro labore
            quos ducimus eaque, qui dolorum sit blanditiis, saepe voluptas reiciendis aperiam cumque
            nisi doloremque? Fugiat quasi rem perspiciatis, illum repellendus expedita suscipit
            commodi. Soluta, repudiandae minima placeat mollitia delectus quia ducimus distinctio
            aspernatur deleniti dolore odio culpa dolor velit amet commodi? Omnis nostrum iste
            recusandae esse ipsum, quasi ad.
          </p>
        </div>
      </article>
    </section>
  </main>
  <footer></footer>
</template>
<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

header {
  height: 200px;
  background: linear-gradient(90deg, rgb(78, 181, 85), hsl(123.2deg 84.27% 17.45%));
  color: white;
}

h1 {
  position: absolute;
  top: 70px;
  right: 300px;
  font-size: 50px;
}

section {
  display: grid;
  grid-template-columns: 30% 70%;
}

body {
  background-color: gainsboro;
}

section > article > div {
  background-color: white;
}

.prio,
.autres {
  width: 50%;
  height: 270px;
  margin: 30px;
  padding: 20px 40px;
  display: inline-block;
  border-radius: 10px;
  background-color: white;
  line-height: 25px;
}

.drapeau {
  position: absolute;
  top: 100px;
  left: 150px;
  border-radius: 10px;
}

.liste {
  position: relative;
  top: 200px;
  width: 300px;
  line-height: 30px;
  left: 50px;
  padding: 15px;
  border-radius: 10px 0px 0px 10px;
  overflow: auto;
  height: 370px;
}

li {
  list-style: none;
  font-weight: bold;
}

.propos {
  padding: 20px;
  margin: 15px;
  line-height: 25px;
  border-radius: 10px;
}

span {
  font-weight: bold;
}

.infos > article {
  display: flex;
  justify-content: space-around;
}

h4 {
  font-weight: 100;
}
a{
    text-decoration: none;
    color: black;
}
</style>
