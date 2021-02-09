<template>
  <div class="tree">
    <ul>
      <TreeItem
        v-for="node in treeData"
        :key="node.id"
        :title="node.name"
        :childrens="node.childrens"
      />
    </ul>
  </div>
</template>

<script>
import TreeItem from "./TreeItem";
export default {
  name: "TreeList",
  components: { TreeItem },
  props: {
    treeData: [Array, Object],
  },
};
</script>

