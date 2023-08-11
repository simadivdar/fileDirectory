<template>
  <div class="tree">
    <ul class="tree-list">
      <node-tree :node="trees"></node-tree>
    </ul>
  </div>
  <div>
  </div>
</template>

<script>
import NodeTree from "./components/NodeTree.vue";


export default {
  data: () => ({
    trees: {
      label: "rooter",
      children: [],
      type: "addFolder",
    },
  }), mounted() {
    console.log(localStorage.trees)
    if (localStorage.getItem('trees')) {
      try {
        this.trees = JSON.parse(localStorage.getItem('trees'));
      } catch (e) {
        localStorage.removeItem('trees');
      }
    }
  },
  methods: {
  },
  components: {
    NodeTree
  }
};
</script>

<style >
.tree-list ul {
  padding-left: 16px;
  margin: 6px 0;
}

.tree {
  background-color: rgb(165, 166, 172);
  padding: 10px;
}
</style>
