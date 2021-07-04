<template>
  <div class="background">
    <div class="sidebar-header">
      <h2>Inventories</h2>
      <a @click="goToCreate"><i class="fas fa-plus"></i></a>
    </div>
    <a
      v-for="inventory in Object.keys(this.$root.$data.store.inventories)"
      :key="inventory"
      :class="activeInventory == inventory ? 'active' : 'disabled'"
      class="inventory-line"
      @click="switchActiveInventory(inventory)"
    >
      {{ inventory }}
    </a>
  </div>
</template>

<script>
export default {
  name: "SideBar",
  created() {},
  computed: {
    activeInventory: function () {
      return this.$root.$data.store.activeInventory;
    },
  },
  methods: {
    switchActiveInventory(newInventory) {
      this.$root.$data.store.activeInventory = newInventory;
      if (this.$route.path !== "/inventory") {
        this.$router.push("/inventory");
      }
    },
    goToCreate() {
      this.$router.push("/create-inventory");
    },
  },
};
</script>

<style scoped>
.background {
  background-color: lightgray;
}
.inventory-line {
  display: block;
  height: 2em;
  line-height: 2em;
  border-bottom: 1px solid darkgray;
}

.inventory-line:hover {
  cursor: pointer;
  background-color: #e9e9e9;
}

.active {
  background-color: white;
}

.active:hover {
  background-color: white;
}

.sidebar-header {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  justify-items: center;
  align-items: center;
}

.sidebar-header > h2 {
  grid-column-start: 2;
  font-weight: bold;
  color: #2c3e50;
}

.sidebar-header > a {
  margin-left: auto;
  padding-right: 10px;
}

.sidebar-header > a:hover {
  cursor: pointer;
  color: gray;
}
</style>
