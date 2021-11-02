<template>
  <div id="app">
    <div class="office">
      <Map @selectTable="handleTableSelect" />
      <SideMenu v-bind.sync="sideMenuData" />
    </div>
  </div>
</template>

<script>
import Map from "./components/Map.vue";
import SideMenu from "./components/SideMenu.vue";
import people from "./assets/data/people.json";
import { find } from "lodash";

export default {
  name: "App",
  components: {
    Map,
    SideMenu,
  },
  data: function () {
    return {
      sideMenuData: {
        isUserOpenned: false,
        person: null,
      },
      people: null,
    };
  },
  created() {
    this.people = people;
  },
  mounted() {
    document.addEventListener("click", this.handleOutsideClick);
  },
  destroyed() {
    document.removeEventListener("click", this.handleOutsideClick);
  },
  methods: {
    handleTableSelect(table) {
      const personData = find(this.people, (man) => man.tableId === table._id);
      this.sideMenuData.person = personData;
      this.sideMenuData.isUserOpenned = true;
    },
    handleOutsideClick(event) {
      if (!event.target.classList.contains("wrapper-table")) {
        this.sideMenuData.isUserOpenned = false;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  background-color: #fafafa;
  padding: 24px;
  box-sizing: border-box;
}

html,
body,
#app {
  height: 100%;
}

* {
  box-sizing: border-box;
}

h3 {
  margin-top: 0px;
}

.office {
  display: grid;
  grid-template-columns: 1fr 320px;
  border-radius: 6px;
  border: 1px solid #ccd8e4;
  height: 100%;
  background: white;
  max-width: 1500px;
  margin: 0 auto;
}
</style>
