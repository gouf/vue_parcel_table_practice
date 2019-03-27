<template>
  <!--
    TODO: 姓・名, 性別など、表示項目の表示・非表示を選別できるインターフェイスをつくる
  -->
  <div v-on:click="toggleFilter">
    <slot></slot>
    <div class="filter" v-on:click="toggleFilter" v-if="filterType === 'text'">
      foo
    </div>
    <div
      class="filter"
      v-on:click="toggleFilter"
      v-if="filterType === 'radioButton'"
    >
      <Radiobutton
        :nameValue="this.nameValue"
        :choises="this.choises"
        v-show="showFilter"
      ></Radiobutton>
    </div>
  </div>
</template>

<script>
import Radiobutton from "./Radiobutton.vue";

export default {
  name: "FilterBox",
  props: {
    // list: Object
    filterType: String,
    relatedWith: String,
    choises: Array,
    nameValue: String
  },
  data() {
    return {
      // showFilter: false
      showFilter: true // for debug
    };
  },
  methods: {
    toggleFilter() {
      this.showFilter = this.showFilter ? false : true;
    }
  },
  computed: {},
  components: {
    Radiobutton
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>

