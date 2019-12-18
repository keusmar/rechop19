<template>
  <div>
    <div class="custom-chart">
      <p class="title">Custom chart</p>
      <table class="content">
        <tr>
          <td>Java</td><td><div title="10%" class="portion portion-10"/></td>
        </tr>
        <tr>
          <td>C#</td><td><div title="20%" class="portion portion-20"/></td>
        </tr>
        <tr>
          <td>Android</td><td><div title="30%" class="portion portion-30"/></td>
        </tr>
        <tr>
          <td>Python</td><td><div title="50%" class="portion portion-50"/></td>
        </tr>
        <tr>
          <td>SQL</td><td><div title="40%" class="portion portion-40"/></td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CustomChart',
  data() {
    return {};
  },
};
</script>

<style src = "./CustomChart.css">
</style>
