<template>
  <div>
    <div class="clickable-list">
      <p class="title">Clickable list</p>
      <div class="pagination-btn">
        <a href="#" title="Previous page" class="circle-btn" id="previous-page">&lt;</a>
        1/10
        <a href="#" title="Next page" class="circle-btn" id="next-page">&gt;</a>
      </div>
      <table class="list">
        <tr>
          <th>first title</th><th>second title</th><th>third title</th><th>fourth title</th>
        </tr>
        <tr>
          <td>1</td><td>2</td><td>3</td><td>4</td>
        </tr>
        <tr>
          <td>1</td><td>2</td><td>3</td><td>4</td>
        </tr>
        <tr>
          <td>1</td><td>2</td><td>3</td><td>4</td>
        </tr>
        <tr>
          <td>1</td><td>2</td><td>3</td><td>4</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ClickableList',
  data() {
    return {};
  },
};
</script>

<style src="./ClickableList.css">
</style>
