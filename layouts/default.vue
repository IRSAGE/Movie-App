<template>
  <div class="app">
    <header class="header">
      <nav>
        <NuxtLink class="link" to="/">Movie App</NuxtLink>
      </nav>
    </header>
    <div><slot /></div>
  </div>
</template>

<style lang="scss" scoped>
.header {
  background-color: #013d5b;
  display: flex;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  height: 64px;
  width: 100%;
  z-index: 10;
  transition: top 0.2s linear;
  nav {
    margin: 10px;
    align-items: center;
  }
  .link {
    text-decoration: none;
    color: white;
    font-weight: bold;
    font-size: 25px;
  }
}
</style>
