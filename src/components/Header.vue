<template>
  <div>
    <header>
      MyMarkdown
    </header>
  </div>
</template>

<script>
export default {
  name: 'Header'
}
</script>

<style lang="scss" scoped>
  header {
    background: #f2f2f2;
    font-weight: bold;
    letter-spacing: .05em;
    padding: 20px;
    text-align: left;
    position: relative;
    display: flex;
    align-items: center;
    &::before {
      background-image: url('../assets/logo.png');
      background-repeat: no-repeat;
      background-size: 100% auto;
      content: '';
      width: 30px;
      height: 30px;
      display: block;
      margin-right: 10px;
    }
  }
</style>