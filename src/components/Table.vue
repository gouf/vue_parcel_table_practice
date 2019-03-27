<template>
  <!--
    TODO: 姓・名, 性別など、表示項目の表示・非表示を選別できるインターフェイスをつくる
    現在「性別」はフィルタ項目をポップアップできる
  -->
  <div>
    <a class="slide" name="tableDataListTop" href="#"></a>
    <table>
      <tr>
        <th v-for="headerItem in headerItems" :key="headerItem.name">
          <FilterBox
            :choises="headerItem.choises"
            :filterType="headerItem.filterType"
            :nameValue="headerItem.relatedWith"
            >{{ headerItem.name }}</FilterBox
          >
        </th>
      </tr>
      <tbody>
        <tr v-for="(data, index) in pageDataSet()" :key="data.id">
          <td v-for="(d, index) in data" :key="d[index]">{{ data[index] }}</td>
        </tr>
      </tbody>
    </table>
    <button v-on:click="rewindToFirstPage" title="Rewind To First Page">
      &lt;&lt;
    </button>
    <button v-on:click="prevPage">back</button> {{ currentPageStart }} -
    {{ currentPageEnd }}/ {{ dataSet.length }}
    <button v-on:click="nextPage">next</button>
  </div>
</template>

<script>
import FilterBox from "./FilterBox";
import headerItemsJson from "../headerItems.json";
import dataSetJson from "../dataSet.json";

export default {
  name: "Table",
  props: {
    // list: Object
  },
  data() {
    return {
      perPage: 20,
      currentPageStart: 1,
      currentPageEnd: 20,
      allRecordsCount: dataSetJson.length,
      headerItems: headerItemsJson,
      dataSet: dataSetJson
    };
  },
  computed: {},
  methods: {
    // Remove ID item from Object safely
    rejectIdItem(dataSet) {
      var ret = dataSet.map(function(obj) {
        var affected = Object.assign(obj);
        delete affected["id"];
        return affected;
      });

      return ret;
    },
    pageDataSet() {
      return this.dataSet.slice(this.currentPageStart - 1, this.currentPageEnd);
    },
    nextPage() {
      if (this.currentPageStart + this.perPage > this.allRecordsCount) {
        return; // 表示範囲値を超える場合に何もしない
      }

      this.currentPageStart += this.perPage;
      this.currentPageEnd += this.perPage;

      this.scrollToTableTop();
    },
    prevPage() {
      if (this.currentPageStart - this.perPage < 0) {
        return; // 表示範囲値を超える場合に何もしない
      }

      this.currentPageStart -= this.perPage;
      this.currentPageEnd -= this.perPage;

      this.scrollToTableTop();
    },
    rewindToFirstPage() {
      this.currentPageStart = 1;
      this.currentPageEnd = this.perPage;

      this.scrollToTableTop();
    },
    scrollToTableTop() {
      document.querySelector('a[name="tableDataListTop"]').scrollIntoView({
        behavior: "smooth"
      });
    }
  },
  components: {
    FilterBox
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
table {
  border: thin solid black;
  border-collapse: collapese;
  border-spacing: 0.01px;
}
table td,
table th {
  border: thin solid #8e8e8e;
}
table td {
  padding: 0.8rem 0.5rem 0.6rem 0.5rem;
}

.slide {
  scroll-behavior: smooth;
  display: block;
}
</style>

