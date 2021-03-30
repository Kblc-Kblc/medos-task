<template>
  <div id="app">
    <div class="wrapper">
      <NavBar />
      <main class="page">
        <div class="_container">
          <Form />
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import NavBar from "@/components/NavBar";
import Form from "@/components/Form";

export default {
  name: "App",
  data() {
    return {};
  },
  components: {
    NavBar,
    Form,
  },
  methods: {},
};
</script>

<style lang="scss">
//<Подключаем шрифты>=======================================================================================
@import url("https://fonts.googleapis.com/css2?family=Rubik:ital,wght@0,400;0,500;0,600;0,700;0,900;1,400&display=swap");
$fontFamily: "Rubik";
//</Шрифт по умолчанию>==========================================================================================

//<ОБНУЛЕНИЕ>===========================================================================================================
* {
  padding: 0px;
  margin: 0px;
  border: 0px;
}
*,
*:before,
*:after {
  box-sizing: border-box;
}
:focus,
:active {
  outline: none;
}
a:focus,
a:active {
  outline: none;
}
aside,
nav,
footer,
header,
section {
  display: block;
}
html,
body {
  height: 100%;
}
body {
  line-height: 1;
  font-family: $fontFamily;
}
input,
button,
textarea {
  font-family: $fontFamily;
}
input::-ms-clear {
  display: none;
}
button {
  cursor: pointer;
}
button::-moz-focus-inner {
  padding: 0;
  border: 0;
}
a,
a:visited {
  text-decoration: none;
}
a:hover {
  text-decoration: none;
}
ul li {
  list-style: none;
}
img {
  vertical-align: top;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  font-weight: inherit;
  font-size: inherit;
}

input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

body {
  color: #fff;
  font-size: 16px;
  letter-spacing: 1px;
}
//</ОБНУЛЕНИЕ>===========================================================================================================

//<ОБОЛОЧКА>===========================================================================================================
.wrapper {
  min-width: 100%;
  width: 100%;
  min-height: 100%;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  //background: #1f212a;
  background: url("./assets/bg.png") 0 0 no-repeat;
  background-size: cover;
}
//</ОБОЛОЧКА>===========================================================================================================

//<ПЕРЕМЕННЫЕ>===========================================================================================================
$minWidth: 320px;
$maxWidth: 1920;
$maxWidthContainer: 479.98;
$md1: $maxWidthContainer + 12;
$md2: 991.98;
$md3: 767.98;
$md4: 479.98;
//</ПЕРЕМЕННЫЕ>===========================================================================================================

//<ОСНОВНАЯ СЕТКА>===========================================================================================================
._container {
  max-width: $maxWidthContainer + px;
  margin: 0 auto;
  @media (max-width: $md1+px) {
    max-width: 970px;
  }
  @media (max-width: $md2+px) {
    max-width: 750px;
  }
  @media (max-width: $md3+px) {
    max-width: none;
    padding: 0 10px;
  }
}
//</ОСНОВНАЯ СЕТКА>===========================================================================================================

//<ОСНОВНОЙ БЛОК>====================================================================================================
.page {
  flex: 1 1 auto;
}
//===================================================================================================================================

//</ОСНОВНОЙ БЛОК>====================================================================================================
</style>
