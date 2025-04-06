<template>
  <Header :header="this.header" />
  <div class="content-container">
    <section class="section-container" id="missions" style="width:435px; height:714px;">
      <div class="section-header clipped-medium-backward">
        <img src="/icons/mission-icon.svg" />
        <h1>Mission Log</h1>
      </div>
      <div class="section-content-container">
        <h3>Current Assignment</h3>
        <Markdown :source="current_md" class="markdown" />
        <h3>Mission List</h3>
        <div class="mission-list-container">
          <Mission
            v-for="item in this.missions"
            :key="item.slug"
            :mission="item"
            :selected="this.mission_slug"
            @click="selectMission(item)"
          />
        </div>
      </div>
    </section>
    <section class="section-container" id="events" style="width:435px; height:714px;">
      <div class="section-header clipped-medium-backward">
        <img src="/icons/events-icon.svg" />
        <h1>Events Log</h1>
      </div>
      <div class="section-content-container">
        <Markdown :source="events" class="markdown" />
      </div>
    </section>
    <section class="section-container" id="pilots" style="width:894px; height:714px;">
      <div style="height:52px; overflow:hidden;">
        <div class="section-header clipped-medium-backward-pilot">
          <img src="/icons/pilot-icon.svg" />
          <h1>Pilot Roster</h1>
        </div>
        <div class="rhombus-back">&nbsp;</div>
      </div>
      <div class="section-content-container">
        <div class="pilot-list-container">
          <Pilot v-for="item in this.pilots" :key="item.slug" :pilot="item" />
        </div>
      </div>
    </section>
  </div>
  <svg
    style="visibility: hidden; position: absolute;"
    width="0"
    height="0"
    xmlns="http://www.w3.org/2000/svg"
    version="1.1"
  >
    <defs>
      <filter id="round">
        <feGaussianBlur in="SourceGraphic" stdDeviation="5" result="blur" />
        <feColorMatrix
          in="blur"
          mode="matrix"
          values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 19 -5"
          result="goo"
        />
        <feComposite in="SourceGraphic" in2="goo" operator="atop" />
      </filter>
    </defs>
  </svg>
  <audio autoplay>
    <source src="/startup.ogg" type="audio/ogg" />
  </audio>
  <Footer/>
</template>

<script>
import Header from './components/layout/Header.vue';
import Footer from './components/layout/Footer.vue';
import Mission from './components/Mission.vue';
import Pilot from './components/Pilot.vue';
import Markdown from 'vue3-markdown-it';

export default {
  components: {
    Header,
    Footer,
    Mission,
    Pilot,
    Markdown
  },

  data() {
    return {
      "mission_slug": "001",
      "current_md": "",
      "events": "",
      "missions": [
        {
          "slug": "001",
          "name": "INVESTIGATE",
          "status": "start"
        },
      ],
      "pilots": [
        {
          "callsign": "CLOVER",
          "alias": "Adam Luckhardt",
          "code": "682e6e6c-d59b-47cc-a8a4-8c9e398b641b//NDL-C-SATELLITE-DECEMBER//5025-04-05T01:36:26.364Z",
          "corpro": "GMS",
          "frame": "Everest",
          "mech": "Cyberpositive"
        },
        {
          "callsign": "FREEBIRD",
          "alias": "Stan Richardson",
          "code": "7cd700cc-c990-48ed-892f-e5468de724c4///NDL-C-DEEP-STATION//a98c3e28-ad4a-4f89-bcd9-501464e960da",
          "corpro": "GMS",
          "frame": "Chomolungma",
          "mech": "Roccoa"
        },
        {
          "callsign": "Thermostat",
          "alias": "Hingy Geitzig",
          "code": "4be26ce9-923b-4069-b6c9-76437d4be455///NDL-C-DEEP-STATION//056940c6-8d55-4190-8e85-57caa043cb1a",
          "corpro": "GMS",
          "frame": "Everest",
          "mech": "Waste_Management"
        },
        {
          "callsign": "POPPY",
          "alias": "William Archer Roosevelt",
          "code": "710728e5-8d40-43dd-8b8e-f2fffe24834c//NDL-C-DEEP-ROYAL//5025-04-05T18:54:36.176Z",
          "corpro": "GMS",
          "frame": "Everest",
          "mech": "Passionate_But_Powerless"
        },
        {
          "callsign": "FALCONER",
          "alias": 'Wei Sen Colello',
          "code": "a1b689d6-bf70-48ff-8d12-c479428b8903//NDL-C-HUNTER'S-ORBIT//5025-04-05T19:36:27.327Z",
          "corpro": "GMS",
          "frame": "Everest",
          "mech": "Skirmisher"
        },
        {
          "callsign": "Map",
          "alias": 'Keta 7.9 Mining',
          "code": "d1fdf62e-d81e-4e10-97c8-df3bc4860117///NDL-C-DEEP-STATION//5a4254aa-9fa2-42ca-a077-8f5bfd1e1ad3",
          "corpro": "GMS",
          "frame": "Everest",
          "mech": "Rio Bravo"
        },
         {
          "callsign": "HANDLER",
          "alias": "M17C",
          "code": "REDACTED-IMOLATECLEARENCEGIVENATCONFLICT279-111",
          "corpro": "GMS",
          "frame": "Everest",
          "mech": "The Bear"
        },
         {
          "callsign": "INDOMITUS",
          "alias": "Vinnie",
          "code": "0faab1fe-945f-4797-a661-53c1c1fc9acf//NDL-C-LIGHT-CRYSTAL//5025-04-06T21:47:06.504Z",
          "corpro": "GMS",
          "frame": "Everest",
          "mech": "BIG VIN"
        },
      ],
      "header": {
        "planet": "Keta 7.9",
        "year": "6019u",
        "system": "Teuflisch",
        "lance": "ROOKIES",
        "ring": "Atriedies-Line",
        "headerTitle": "Teuflisch",
        "headerSubtitle": "Special Operations",
        "subheaderTitle": "Division",
        "subheaderSubtitle": "BATTLENET.V.3.54B",
      },
      "options":{
        "eventsMarkdownPerMission": true
      }
    }
  },

  created() {
    this.loadMissionMarkdown()
    this.loadEventsMarkdown()
  },

  computed: {

  },

  methods: {
    selectMission(mission) {
      this.mission_slug = mission.slug;
      this.loadMissionMarkdown()
      if(this.options.eventsMarkdownPerMission){
        this.loadEventsMarkdown();
      }
    },
    loadMissionMarkdown() {
      let self = this;
      let md = `/missions/${self.mission_slug}.md`
      var client = new XMLHttpRequest();
      client.open('GET', md);
      client.onreadystatechange = function () {
        self.current_md = client.responseText;
      }
      client.send();
    },
    loadEventsMarkdown() {
      let self = this;
      let md = "";

      if(self.options.eventsMarkdownPerMission){
        md = `/events/${self.mission_slug}.md`
      }
      else {
        md = "/events.md"
      }

      var client = new XMLHttpRequest();
      client.open('GET', md);
      client.onreadystatechange = function () {
        self.events = client.responseText;
      }
      client.send();
    }
  }

}
</script>


<style lang="scss">
#app {
  width: 1902px;
  height: 910px;
  overflow: hidden;
}
</style>
