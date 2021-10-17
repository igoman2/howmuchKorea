<template>
  <div class="text-center">
    <!-- <div>
      <v-data-table
        :headers="headers"
        :items="desserts"
        :items-per-page="5"
        class="elevation-1"
      ></v-data-table>
    </div> -->
    <div
      style="background-color:yellow; position:relative; width:800px; height:1000px"
    >
      <radio-svg-map
        :map="Korea"
        v-model="selectedLocations"
        :location-class="getLocationClass"
        @mouseover="pointLocation"
        @mouseout="unpointLocation"
        @mousemove="moveOnLocation"
      />
      <div style="color: red !important; position:absolute; top:14%; left:25%">
        <h1>
          {{ seoul }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:17%; left:12%">
        <h1>
          {{ incheon }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:22%; left:28%">
        <h1>
          {{ gg }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:30%; left:40%">
        <h1>
          {{ chungbuk }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:37%; left:23%">
        <h1>
          {{ chungnam }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:65%; left:25%">
        <h1>
          {{ jeonnam }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:50%; left:30%">
        <h1>
          {{ jeonbuk }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:58%; left:25%">
        <h1>
          {{ gwangju }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:15%; left:50%">
        <h1>
          {{ gangwon }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:33%; left:30%">
        <h1>
          {{ sejong }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:37%; left:35%">
        <h1>
          {{ daejeon }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:55%; left:50%">
        <h1>
          {{ gn }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:35%; left:55%">
        <h1>
          {{ gb }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:45%; left:55%">
        <h1>
          {{ daegu }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:50%; left:65%">
        <h1>
          {{ ulsan }}
        </h1>
      </div>
      <div style="color: red !important; position:absolute; top:62%; left:65%">
        <h1>
          {{ busan }}
        </h1>
      </div>
      <div
        style="color: red !important; position:absolute; bottom:8%; left: 16%"
      >
        <h1>
          {{ jeju }}
        </h1>
      </div>
      <div class="examples__block__map__tooltip" :style="tooltipStyle">
        <span style="color:black !important">
          <span v-if="pointedLocation == 'Gyeonggi'">
            {{ gg }}
          </span>
          <span v-else-if="pointedLocation == 'Seoul'">
            {{ seoul }}
          </span>
          <span v-else-if="pointedLocation == 'Gangwon'">
            {{ gangwon }}
          </span>
          <span v-else-if="pointedLocation == 'North Gyeongsang'">
            {{ gb }}
          </span>
          <span v-else-if="pointedLocation == 'South Gyeongsang'">
            {{ gn }}
          </span>
          <span v-else-if="pointedLocation == 'Daegu'">
            {{ daegu }}
          </span>
          <span v-else-if="pointedLocation == 'Ulsan'">
            {{ ulsan }}
          </span>
          <span v-else-if="pointedLocation == 'Busan'">
            {{ busan }}
          </span>
          <span v-else-if="pointedLocation == 'South Jeolla'">
            {{ jeonnam }}
          </span>
          <span v-else-if="pointedLocation == 'North Jeolla'">
            {{ jeonbuk }}
          </span>
          <span v-else-if="pointedLocation == 'Gwangju'">
            {{ gwangju }}
          </span>
          <span v-else-if="pointedLocation == 'Jeju'">
            {{ jeju }}
          </span>
          <span v-else-if="pointedLocation == 'Deajeon'">
            {{ deajeon }}
          </span>
          <span v-else-if="pointedLocation == 'Sejong'">
            {{ sejong }}
          </span>
          <span v-else-if="pointedLocation == 'North Chungcheong'">
            {{ chungbuk }}
          </span>
          <span v-else-if="pointedLocation == 'South Chungcheong'">
            {{ chungnam }}
          </span>
          <span v-else-if="pointedLocation == 'Incheon'">
            {{ incheon }}
          </span>
          <span v-else-if="pointedLocation == 'Daejeon'">
            {{ daejeon }}
          </span>
        </span>
      </div>
      <!-- <checkbox-svg-map v-model="selectedLocations" :map="Korea" /> -->
    </div>
  </div>
</template>

<script>
import { SvgMap } from "vue-svg-map";
import { getLocationName } from "@/utilities/index";
import { RadioSvgMap } from "vue-svg-map";
import Korea from "@svg-maps/south-korea";

export default {
  name: "MyMap",
  components: {
    SvgMap,
    RadioSvgMap
  },
  data() {
    return {
      seoul: 1405,
      busan: 451,
      daegu: 398,
      incheon: 546,
      gwangju: 395,
      daejeon: 453,
      ulsan: 360,
      gg: 674,
      gangwon: 246,
      chungbuk: 256,
      chungnam: 262,
      jeonbuk: 233,
      jeonnam: 238,
      sejong: 632,
      gb: 239,
      gn: 303,
      jeju: 414,

      headers: [
        {
          text: "Dessert (100g serving)",
          align: "start",
          sortable: false,
          value: "name"
        },
        { text: "Calories", value: "calories" },
        { text: "Fat (g)", value: "fat" },
        { text: "Carbs (g)", value: "carbs" },
        { text: "Protein (g)", value: "protein" },
        { text: "Iron (%)", value: "iron" }
      ],
      desserts: [
        {
          name: "Frozen Yogurt",
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: "1%"
        },
        {
          name: "Ice cream sandwich",
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: "1%"
        },
        {
          name: "Eclair",
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: "7%"
        },
        {
          name: "Cupcake",
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: "8%"
        },
        {
          name: "Gingerbread",
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          iron: "16%"
        },
        {
          name: "Jelly bean",
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: "0%"
        },
        {
          name: "Lollipop",
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: "2%"
        },
        {
          name: "Honeycomb",
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: "45%"
        },
        {
          name: "Donut",
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          iron: "22%"
        },
        {
          name: "KitKat",
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: "6%"
        }
      ],
      Korea,
      selectedLocations: "",
      pointedLocation: null,
      tooltipStyle: null
    };
  },
  methods: {
    pointLocation(event) {
      this.pointedLocation = getLocationName(event.target);
    },
    unpointLocation(event) {
      this.pointedLocation = null;
      this.tooltipStyle = { display: "none" };
    },
    moveOnLocation(event) {
      this.tooltipStyle = {
        display: "block",
        top: `${event.clientY + 10}px`,
        left: `${event.clientX - 100}px`
      };
    },
    focusLocation(event) {
      this.focusedLocation = getLocationName(event.target);
    },
    blurLocation(event) {
      this.focusedLocation = null;
    },
    getLocationClass(location, index) {
      // Generate heat map
      return `svg-map__location svg-map__location--heat${index % 4}`;
    }
  }
};
</script>

<style src="vue-svg-map/dist/index.css"></style>
