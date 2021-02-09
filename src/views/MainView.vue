<template>
  <div class="main">
    <TreeList :treeData="tree" v-if="tree" />
  </div>
</template>

<script>
import TreeList from "../components/TreeList";
export default {
  name: "MainView",
  components: {
    TreeList,
  },
  data() {
    return {
      tree: [],
    };
  },
  methods: {
    async getJsonData() {
      let response = await fetch("https://nefteavtomat.herokuapp.com/json", {
        method: "GET",
      });
      let result = await response.json();
      this.tree = this.createTree(result);
      return result;
    },

    createTree(data) {
      const tempTree = {};
      data.forEach((parrent) => {
        tempTree[parrent.id] = parrent;
        tempTree[parrent.id].childrens = [];
      });

      const resultTree = [];
      data.forEach((child) => {
        if (child.pid !== 0) {
          tempTree[child.pid].childrens.push(tempTree[child.id]);
        } else {
          resultTree.push(tempTree[child.id]);
        }
      });
      return resultTree;
    },
  },
  created() {
    this.getJsonData();
  },
};
</script>

<style>
</style>