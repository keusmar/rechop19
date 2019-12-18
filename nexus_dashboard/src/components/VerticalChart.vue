<template>
  <div>
    <div class="vertical-chart">
      <p class="title">Vertical chart</p>
      <table class="content">
        <tr>
          <td><div title="10%" class="portion portion-10"/></td>
          <!-- <td>a</td> -->
          <td><div title="20%" class="portion portion-20"/></td>
          <!-- <td></td> -->
          <td><div title="30%" class="portion portion-30"/></td>
          <!-- <td></td> -->
          <td><div title="50%" class="portion portion-50"/></td>
          <!-- <td></td> -->
          <td><div title="40%" class="portion portion-40"/></td>
          <!-- <td></td> -->
        </tr>
        <tr>
          <td>Java</td>
          <td>C#</td>
          <td>Python</td>
          <td>SQL</td>
          <td>Android</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VerticalChart',
  data() {
    return {};
  },
};
</script>

<style src = "./VerticalChart.css">
</style>
