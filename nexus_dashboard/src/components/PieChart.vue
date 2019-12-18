<template>
  <div class="floating-box">
    <p class="title">
      Pie chart
    </p>
    <div class="pieContainer">
      <div class="pieBackground"></div>
      <div id="pieSlice1" class="hold">
        <div class="pie"></div>
      </div>
      <div id="pieSlice2" class="hold">
        <div class="pie"></div>
      </div>
      <div id="pieSlice3" class="hold">
        <div class="pie"></div>
      </div>
      <div id="pieSlice4" class="hold">
        <div class="pie"></div>
      </div>
      <div id="pieSlice5" class="hold">
        <div class="pie"></div>
      </div>
      <div class="innerCircle">
      </div>
    </div>
    <div class="code-Container">
      <table class="code-table">
        <tr>
          <td><div class="colorcode pieSlice1Color"/></td><td>Java</td>
        </tr>
        <tr>
          <td><div class="colorcode pieSlice2Color"/></td><td>C#</td>
        </tr>
        <tr>
          <td><div class="colorcode pieSlice3Color"/></td><td>Android</td>
        </tr>
        <tr>
          <td><div class="colorcode pieSlice4Color"/></td><td>Python</td>
        </tr>
        <tr>
          <td><div class="colorcode pieSlice5Color"/></td><td>SQL</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PieChart',
  data() {
    return {};
  },
};
</script>

<style src = "./PieChart.css">
</style>
