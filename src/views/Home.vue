<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    {{ msg }}
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  data: function() {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>
