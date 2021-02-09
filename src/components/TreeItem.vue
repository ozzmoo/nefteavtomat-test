<template>
  <li class="item">
    <span @click="toogleNode">
      <span
        v-if="isShowNode"
        :class="[!childrens.length ? 'marker--empty' : '', 'marker']"
      >
        ▼
      </span>
      <span
        v-else
        :class="[!childrens.length ? 'marker--empty' : '', 'marker']"
      >
        ▶
      </span>
      {{ title }}
    </span>
    <transition name="fade">
      <ul v-if="childrens" v-show="isShowNode">
        <TreeItem
          v-for="child in childrens"
          :key="child.id"
          :title="child.name"
          :childrens="child.childrens"
        />
      </ul>
    </transition>
  </li>
</template>

<script>
export default {
  name: "TreeItem",

  props: {
    title: {
      type: String,
      default: "",
    },
    childrens: {
      type: Array,
      default: () => {
        [];
      },
    },
  },
  data() {
    return {
      isShowNode: false,
    };
  },
  methods: {
    toogleNode() {
      this.isShowNode = !this.isShowNode;
    },
  },
};
</script>

<style scoped>
.item {
  cursor: pointer;
  line-height: 1.2rem;
  font-size: 1.2rem;
  padding: 0.5rem;
}
.item::marker {
  content: "";
}

.marker--empty {
  opacity: 0;
}

/* animations */
.fade-enter-active,
.fade-leave-active {
  transition: 0.3s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>