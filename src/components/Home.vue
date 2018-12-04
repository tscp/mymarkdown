<template>
  <div id="home">
    <h1>{{ msg }}</h1>
    <p>This (TEST) Site Powered by <a href="https://vuejs.org/">Vue.js</a> + <a href="https://firebase.google.com/">Firebase</a> + <a href="https://github.com">Github</a> + <a href="https://www.netlify.com/">Netlify</a></p>
    <button @click="googleLogin">Google アカウントでログイン</button>
  </div>
</template>

<script>
  export default {
    name: "home",
    data() {
      return {
        msg: "Simple Markdown Editor"
      };
    },
    methods: {
      googleLogin: function() {
        firebase
          .auth()
          .signInWithRedirect( new firebase.auth.GoogleAuthProvider() );
      }
    },
  };
</script>

<style lang="scss" scoped>
  div {
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    height: 80vh;
  }
  h1 {
    font-size: 4rem;
    font-weight: bold;
    margin: 10px;
  }
  p {
    padding: 20px;
  }
  button {
    border: #fff;
    border-radius: 40px;
    box-shadow: 0 2px 8px rgba(0,0,0,.2);
    background: #f2f2f2;
    color: #666;
    cursor: pointer;
    padding: 10px 40px;
    margin: 10px;
    &:hover {
      background: #efefef;
    }
  }
</style>