<template>
  <v-app>
    <v-app-bar app color="secondary" dark>
      <div class="d-flex align-center">
        <h2>SpaceX History</h2>
      </div>

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-content>
      <v-container>
        <v-timeline v-if="launches.length > 0">
          <Launch
            v-for="launch in launches"
            :key="launch.flight_number"
            :launch="launch"
          />
        </v-timeline>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import axios from "axios";
import Launch from "./components/Launch";
export default {
  name: "App",

  components: {
    Launch,
  },

  data: () => ({
    launches: [],
  }),
  async created() {
    const { data } = await axios.get("https://api.spacexdata.com/v3/launches");

    data.forEach((launch) => {
      this.launches.push(launch);
    });

    console.log(this.launches);
  },
};
</script>
