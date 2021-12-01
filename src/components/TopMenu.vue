<template>
  <ul class="main-menu">
    <li><router-link to='/'>Home</router-link></li>
    <li><router-link to='/todo'>Todo</router-link></li>
  </ul>
</template>

<style scoped lang="scss">
  .main-menu {
    list-style: none;
    display: flex;
    justify-content: center;
    align-items: center;
    a{
      margin: 10px;
      text-decoration: none;
      text-transform: uppercase;
      color: #2c3e50;
    }
  }
</style>