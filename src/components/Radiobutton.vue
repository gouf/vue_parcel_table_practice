<template>
  <div>
    <form>
      <div class="choise-group" v-for="value in choises" :key="value">
        <input :name="nameValue" :id="value" type="radio" value="value" />
        <label for="value">{{ value }}</label>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "Radiobutton",
  props: {
    choises: Array,
    nameValue: String
  },
  data() {
    return {};
  },
  components: {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.choise-group {
  background: none;
  position: relative;
}
div {
  padding-top: 1rem;
  position: absolute;
  background: #fefefe;
}
form {
  padding: 1rem;
  overflow: scroll;
  border: thin solid #0a0a0a;
}
</style>

