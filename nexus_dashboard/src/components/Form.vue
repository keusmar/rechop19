<template>
  <div>
    <div class="floating-form">
      <p class="title">Form</p>
      <form action="#">
        <table>
            <tr>
              <td><input type="text" placeholder="login"></td>
            </tr>
            <tr>
              <td><input type="password" placeholder="password"></td>
            </tr>
            <tr>
              <td>
                <input type="radio" name="gender" id="male" value="male">
                <label for="male" class="text">Male</label>
              </td>
            </tr>
            <tr>
              <td>
                <input type="radio" name="gender" id="female" value="female">
                <label for="female" class="text">Female</label>
              </td>
            </tr>
            <tr>
              <td>
                <label class="text" for="">Language :</label>
                <select>
                  <option value="Java">Java</option>
                  <option value="C#">C#</option>
                  <option value="Python">Python</option>
                  <option value="Android">Android</option>
                </select>
              </td>
            </tr>
        </table>
        <a href="" class="round-btn">submit</a>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Form',
  data() {
    return {};
  },
};
</script>

<style src="./Form.css">
</style>
