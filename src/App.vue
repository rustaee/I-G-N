<template>
  <div class="container">
    <!-- Header -->
    <header>
        <h1>Please enter your license plate number</h1>
        <div class="plate">
          <form @submit.prevent="getCarInfo()">
            <input type="text" class="plate__input" v-model="plateNumber">
            <button class="plate__sendbtn" type="submit">Send</button>
          </form>
        </div>
    </header>

    <!--API -->
    <div class="api">
      <div class="api__result">
        <!-- Error --> 
        <div v-if="error" class="error">
          <h3>We couldn't find any information.</h3> 
            <p>please make sure you've entered the right plate number</p>
        </div>

        <!-- Loading -->
        <div v-else-if="loading" class="loading">
          <font-awesome-icon icon="spinner" />
        </div>

        
        <!-- Data -->
        <div v-else class="data">
          <div class="api__title" v-if="!admissionDate">enter plate number to get these information.</div>
          <div class="info">
            <div class="info__title">Trade name</div>
            <div class="info__value">{{ tradeName }}</div>
          </div>

          <div class="info">
            <div class="info__title">Date of first admission</div>
            <div class="info__value">{{ admissionDate}}</div>
          </div>

          <div class="info">
            <div class="info__title">Fuel description</div>
            <div class="info__value">{{ fuel }}</div>
          </div>
        </div>

      </div>
    </div>

    <!--Slider -->
    <div class="slider">
      <div class="slider--prev"><font-awesome-icon icon="chevron-left" /></div>
      <div class="slides-container">
        <div class="slides">
          <img src="/images/header.jpg" alt="" />
          <img src="/images/car.jpg" alt="" />
          <img src="/images/car2.jpg" alt="" />
        </div>
      </div>
      <div class="slider--next"><font-awesome-icon icon="chevron-right" /></div>
    </div>

    <!-- Footer -->
    <footer>
      <p>Copyright <span>&copy;</span> 2020-2021 All rights reserved</p>
    </footer>
  </div>
</template>
<script>
export default {
  data(){
    return{
      apiKey: '76d237b0f1cc4a6ddaa41f79cd3345fc09c2c0a2b907ad7184d775b2615b6b3f',
      apiUrl: 'https://api.overheid.io/voertuiggegevens',
      plateNumber: null,
      tradeName: null,
      admissionDate: null,
      fuel: null,
      error: false,
      loading: false,
    }
  },
  mounted(){
    fetch('https://api.unsplash.com/search/photos?page=1&query=office')
    .then(response => response.json())
    .then(data => console.log(data))
  },
  methods: {
    getCarInfo(){
      this.loading = true,
      this.error = false,

      fetch(`${this.apiUrl}/${this.plateNumber}?ovio-api-key=${this.apiKey}`)
      .then(response => response.json())
      .then(data => {
        this.loading = false;
        this.tradeName = data.handelsbenaming;
        this.admissionDate = data.datum_eerste_toelating,
        this.fuel = data.brandstof[0]['brandstof_omschrijving'];
      })
      .catch(error => {
        this.error = true
        console.log(error);
        })
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap');
$font-roboto: 'Roboto', sans-serif;
$font-size: 14px;
$font-color: #474747;
$bg: #f6f6f6;
$primary-color: #ae4c03;


*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

input, button {
  outline: none;
  border: none;
}

body{
  font-family: $font-roboto;  
  background: $bg;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $font-color;
  font-size: $font-size;
  line-height: 30px;
  overflow-x: hidden;
}

.container{
  width: 100vw;
  display: grid;
  grid-template: auto 300px 1fr auto/ 1fr;
  grid-template-areas: "header"
  "api"
  "slider"
  "footer";
}

header{
  width: 100vw;
  grid-area: header;
  background-color: rgb(107, 107, 107);
  background-image: url('assets/header.jpg');
  background-blend-mode: multiply;
  background-position: center;
  background-size: cover;
  padding: 50px 20px 80px 20px;

  h1{
    color: #fff;
    font-size: 1.4rem;
  }
}

.plate{
  margin: 15px 0;

  form{
  display: flex;
  justify-content: center;
  }
}

.plate__input{
  background: #f6d781;
  border: none;
  padding: 10px;
  width: 45%;
  font-size: 1.2rem;
  font-weight: 800;
  color: $font-color;
}

.plate__sendbtn{
  width: 15%;
  background: #fdfdfd;
  font-weight: 700;
  color: $font-color;
  cursor: pointer;
}

/** Api */
.api{
  grid-area: api;
  display: flex;
  justify-content: center;
  position: relative;
}

.api__title{
  text-align: center;
  color: $primary-color;
  line-height: 20px;
  font-size: $font-size - 2px;
}

.api__result{
  width: 80%;
  background: #fff;
  box-shadow: 0px 5px 5px rgba(0, 0, 0, 0.1);
  padding: 20px;
  text-align: left;
  border-radius: 10px;
  position: absolute;
  top: -50px;
}

.info{
  margin-bottom: 20px;
}

.info__title{
  font-weight: 600;
  line-height: 30px;
  color: #5e5e5e;
}

.info__value{
  font-size: $font-size + 10px;
  font-weight: bold;
}

.error{
  color: rgb(182, 14, 14);
}

/** Slider */
.slider{
  grid-area: slider;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.slides-container{
 width: 75%;
 height: 100%;
 position: relative;
 overflow: hidden;
}

.slider--prev,
.slider--next{
  width: 10%;
  font-size: 1.5rem;

  &:hover{
    color: $primary-color;
    cursor: pointer;
  }
}

.slides{
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  height: 100%;
  width: 300%;

  img{
    width: 100%;
    height: 100%;
    object-fit: cover;
    width: 33%;
     margin: 0 5px;
  }
}

footer {
  grid-area: footer;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  background-color: $primary-color;
  color: #fff;
  margin-top: 20px;
  font-size: $font-size - 1px;

  span {
    color: #000;
  }
}

.loading{
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 40px;
  color: $primary-color;
  animation: spinner 0.7s steps(4) infinite;
}

@keyframes spinner {
  0% {
    transform: rotate(0deg);
  }

  50% {
    transform: rotate(180deg);
  }

  100% {
    transform: rotate(360deg);
  }
}


@media (min-width: 765px){
  .slides{
    width: 150%;
  }
  header{
    height: 50vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .plate{
    width: 60%;
  }

  .api__result{
    width: 60%;
  }

  .api__title{
    font-size: 1rem;
    font-weight: bold;
    margin-bottom: 20px;
  }

  .error{
    text-align: center;
  }

}

@media (min-width: 1024px) {

  body{
    font-size: $font-size + 2px;
  }

  header{
    h1{
      font-size: 2rem;
    }
  }

  .plate{
    margin: 30px 0;
    width: 40%;
  }

  .plate__input,
  .plate__sendbtn{
    font-size: 1.5rem;
  }

  .plate__sendbtn{
    width: 20%;
  }
  
  .slides{
    width: 100%;
  }
  
  .api__result{
    width: 40%;
    font-size: 1.3rem;
  }

  .info__value{
    font-size: 2rem;
    margin-top: 10px;
  }
}

</style>
