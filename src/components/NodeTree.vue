<template>
  <li class="node-tree">
    <details :class="{ style: hey }" open>
      <summary class="collapse">
        <span class="label">{{ node.label }}</span>
        <div class="set-btn">
          <div v-show="node.type === 'addFolder'">
            <button class="btn" @click="changeStateInput('addFolder')"><svg width="20" height="20" viewBox="0 0 24 24"
                fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M11 14.5V16.5H13V14.5H15V12.5H13V10.5H11V12.5H9V14.5H11Z" fill="currentColor" />
                <path fill-rule="evenodd" clip-rule="evenodd"
                  d="M4 1.5C2.89543 1.5 2 2.39543 2 3.5V4.5C2 4.55666 2.00236 4.61278 2.00698 4.66825C0.838141 5.07811 0 6.19118 0 7.5V19.5C0 21.1569 1.34315 22.5 3 22.5H21C22.6569 22.5 24 21.1569 24 19.5V7.5C24 5.84315 22.6569 4.5 21 4.5H11.874C11.4299 2.77477 9.86384 1.5 8 1.5H4ZM9.73244 4.5C9.38663 3.9022 8.74028 3.5 8 3.5H4V4.5H9.73244ZM3 6.5C2.44772 6.5 2 6.94772 2 7.5V19.5C2 20.0523 2.44772 20.5 3 20.5H21C21.5523 20.5 22 20.0523 22 19.5V7.5C22 6.94772 21.5523 6.5 21 6.5H3Z"
                  fill="currentColor" />
              </svg></button>
            <button class="btn" @click="changeStateInput('addFile')"><svg width="20" height="20" viewBox="0 0 24 24"
                fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M10 18V16H8V14H10V12H12V14H14V16H12V18H10Z" fill="currentColor" />
                <path fill-rule="evenodd" clip-rule="evenodd"
                  d="M6 2C4.34315 2 3 3.34315 3 5V19C3 20.6569 4.34315 22 6 22H18C19.6569 22 21 20.6569 21 19V9C21 5.13401 17.866 2 14 2H6ZM6 4H13V9H19V19C19 19.5523 18.5523 20 18 20H6C5.44772 20 5 19.5523 5 19V5C5 4.44772 5.44772 4 6 4ZM15 4.10002C16.6113 4.4271 17.9413 5.52906 18.584 7H15V4.10002Z"
                  fill="currentColor" />
              </svg></button>
          </div>
          <div>
          <button class="btn" id="sima" @click="deletef(node)"><svg width="20" height="20" viewBox="0 0 24 24" fill="none"
              xmlns="http://www.w3.org/2000/svg">
              <path
                d="M8 11C7.44772 11 7 11.4477 7 12C7 12.5523 7.44772 13 8 13H16C16.5523 13 17 12.5523 17 12C17 11.4477 16.5523 11 16 11H8Z"
                fill="currentColor" />
              <path fill-rule="evenodd" clip-rule="evenodd"
                d="M23 12C23 18.0751 18.0751 23 12 23C5.92487 23 1 18.0751 1 12C1 5.92487 5.92487 1 12 1C18.0751 1 23 5.92487 23 12ZM21 12C21 16.9706 16.9706 21 12 21C7.02944 21 3 16.9706 3 12C3 7.02944 7.02944 3 12 3C16.9706 3 21 7.02944 21 12Z"
                fill="currentColor" />
            </svg></button>
          </div>
        </div>
        <input v-model="tree.label" @keyup.enter="add()" v-bind:hidden="hide" />
      </summary>
      <ul v-if="node.children && node.children.length">
        <node v-for="(child, index) in node.children" :node="child" :key="index"></node>
      </ul>
    </details>
  </li>
  <div class="set" v-if="node.label == 'rooter'">
    <button class="btn" @click="newDirectory()">Update</button>
    <button class="btn" @click="persist()">save</button>
  </div>
</template>
  
<script>
export default {
  name: "node",
  data: () => ({
    tree: {
      label: "",
      children: [],
      type: "",
    },
    hide: true,
    addF: "",
    hey: false
  }),
  props: {
    node: Object,
  },
  computed: {
    changeState() {
      console.log("hi");
    },
  },
  methods: {
    add() {
      if (this.addF == "addFolder") {
        console.log(this.addF)
        this.node.children.push({ label: this.tree.label, children: this.tree.children, type: "addFolder" });
      }
      else {
        console.log(this.addF)
        this.node.children.push({ label: this.tree.label, type: "addFile" });
      }
      this.tree.children = [];
      this.tree.label = "";
      this.hide = true;
    },
    changeStateInput(name) {
      this.hide = !this.hide;
      this.addF = name;
    },
    deletef(event) {
      console.log( event.children);
      event.children=""
    },
    persist() {
      localStorage.trees = JSON.stringify(this.node);
      console.log('now pretend I did more stuff...');
    },
    newDirectory() {
      localStorage.removeItem('trees');
    }
  }
};
</script>
<style>
.collapse {
  padding: 2px 6px;
  width: 15em;
  background-color: #ddd;
  border: none;
  box-shadow: 1px 1px 3px black;
  cursor: pointer;
}

.style {
  list-style: none;
}

.btn {
  margin: 0px 2px -6px;
  color: rgb(255, 127, 202);
  border: 0px;
  background-color: #ddd;
  cursor: pointer;
}

.set {
  margin-top: 20px;
  display: flex;
}
.set-btn{
  display: flex;
  justify-content: flex-end;
}</style>