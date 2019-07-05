
<template>
    <div id="app">
        <h1>Calculator</h1>
        <calculator />
    </div>    
</template>

<script>
import calculator from './main/calculator';

export default {
  components: {
    calculator
  }

}
</script>

<style>
  @font-face {
    font-family: "RobotoMono";
    src: url('./fonts/RobotoMono-Thin.ttf');
  }
  * {
    font-family: "RobotoMono", monospace;
  }
  body {
    margin: 0;
  }
  #app {
    color: #fff;
    display: flex;
    height: 100vh;
    text-align: center;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    background: linear-gradient(to right, rgb(83, 105, 118), rgb(41, 46, 73));
  }
</style>
