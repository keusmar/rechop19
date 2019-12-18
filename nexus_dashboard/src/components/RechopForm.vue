<template>
  <div>
    <div class="floating-form">
      <p class="title">Paramètres</p>
      <form action="#">
        <table>
            <tr>
              <td><input type="text" placeholder="Germe (x0)"></td>
            </tr>
            <tr>
              <td><input type="text" placeholder="a"></td>
            </tr>
            <tr>
              <td><input type="text" placeholder="c"></td>
            </tr>
            <tr>
              <td><input type="text" placeholder="m"></td>
            </tr>
        </table>
        <a href="" class="round-btn" @click.prevent="$parent.simulation">submit</a>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RechopForm',
  data() {
    return {};
  },
};
</script>

<style src="./Form.css">
</style>
