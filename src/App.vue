<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div>
        <h2>SpaceX Timeline</h2>
      </div>

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-main style="max-width: 80%; margin: 0 auto">
      <v-timeline v-if="launches.length > 0">
        <LaunchTimelineItem
          v-for="launch in launches"
          :key="launch.flight_number"
          :launch="launch"
        />
      </v-timeline>
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";

import LaunchTimelineItem from "./components/LaunchTimelineItem.vue";

export default {
  name: "App",

  components: {
    LaunchTimelineItem,
  },

  data: () => ({
    launches: [],
  }),
  async created() {
    const { data } = await axios.get("https://api.spacexdata.com/v3/launches");
    data.forEach((launch) => {
      this.launches.push(launch);

      console.log(this.launches);
    });
  },
};
</script>
