<template>
  <div class="container">
    <!-- Header -->
    <header>
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
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #1c1c1c;
}

.container{
  width: 100vw;
  height: 100vh;
  display: grid;
  grid-template: minmax(100px, auto) 30% 30% minmax(50px, 10%)/ 1fr;
  grid-template-areas: "header"
  "api"
  "slider"
  "footer";
}

header{
  width: 100vw;
  grid-area: header;
  background-color: #555;
  background-image: url('assets/header.jpg');
  background-blend-mode: multiply;
  background-position: center;
  background-size: cover;
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
  box-shadow: 0px 5px 5px rgba(0, 0, 0, 0.2);
  padding: 20px;
  text-align: left;
  border-radius: 10px;
  position: absolute;
  top: -40px;
}

.slider{
  grid-area: slider;
  background-color: green;
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
