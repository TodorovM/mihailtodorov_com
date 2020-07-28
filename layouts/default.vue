<template>
  <div>
    <HamburgerMenu />
    <Nuxt />
  </div>
</template>
<style>
:root {
  --background-color: #1b1b2f;
  --font-color: #ececec;
  --red-color: #e43f5a;
  --background-secondary-color: #162447;
  --background-third-color: #1f4068;
}


html {
  font-family: 'Roboto Condensed', sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  background-color: var(--background-color);
  color: var(--font-color);
}



*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

</style>
