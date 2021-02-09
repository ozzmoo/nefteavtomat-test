<template>
  <div class="tree">
    <ul>
      <li v-for="item in treeData" :key="item.id">
        {{ item.name }}
        <ul v-if="item.childrens.length > 0 && showNode">
          <TreeList :treeData="item.childrens" />
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TreeList",
  props: {
    treeData: [Array, Object],
  },

  data() {
    return {
      showNode: true,
    };
  },
  methods: {
    toogleNode() {
      this.showNode = !this.showNode;
      console.log("clicked");
    },
  },
};
</script>

<style>
</style>

