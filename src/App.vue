<template>
  <div class="container">
    <!-- Header -->
    <header>
        <h1>Please enter your license plate number</h1>
        <div class="plate">
          <input type="text" class="plate__input">
          <button class="plate__sendbtn">Send</button>
        </div>
    </header>
    <!--API -->
    <div class="api">
      <div class="api__result">
        dfdsd
      </div>
    </div>
    <!--Slider -->
  <div class="slider">
    <div class="slider--prev"></div>
    <div class="slides-container"></div>
    <div class="slider--next"></div>
  </div>
    <!-- Footer -->
    <footer>
      Footer
    </footer>
  </div>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap');
$font-roboto: 'Roboto', sans-serif;
$font-color: #474747;
$bg: #f6f6f6;

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

input, button {
  outline: none;
  border: none;
}

#app {
  font-family: $font-roboto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $font-color;
  background: $bg;
}

.container{
  width: 100vw;
  height: 100vh;
  display: grid;
  grid-template: auto 30% 30% minmax(50px, 10%)/ 1fr;
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
  display: flex;
  justify-content: center;
  margin: 15px 0;
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
}

.api{
  grid-area: api;
  display: flex;
  justify-content: center;
  position: relative;

}

.api__result{
  width: 80%;
  height: 100%;
  background: #fff;
  box-shadow: 0px 5px 5px rgba(0, 0, 0, 0.1);
  padding: 20px;
  text-align: left;
  border-radius: 10px;
  position: absolute;
  top: -40px;
}

.slider{
  grid-area: slider;
  background-color: rgb(126, 187, 126);
  display: flex;
  justify-content: space-between;
}

.slides-container{
 width: 75%;
 background: yellow;
}

.slider--prev,
.slider--next{
  width: 10%;
  background: red;
}


footer{
  grid-area: footer;
  background-color: red
}

</style>
