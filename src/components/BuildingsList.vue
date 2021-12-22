<template>
    <div class="buildings-list pt-3">
    <buildings-list-item 
      v-for="building in buildings"
      :building="building"
      :key="building.id"  
    >
    </buildings-list-item>
  </div>
</template>

<script>
import axios from 'axios';
import BuildingsListItem from './BuildingsListItem';

export default {
  components: {
    BuildingsListItem
  },
  name: 'BuildingsList',
  data: function() {
    return {
      buildings: []
    }
  },
  created: async function() {
    let response = await axios.get('https://farid-bechaalany.cleverapps.io/api/buildings');
    let buildings = response.data;
    this.buildings = buildings;
  }
}
</script>