<template>
  <div class="window border border-secondary rounded p-2 mb-2" :class="{expanded: isExpanded}">
    <div class="top-row d-flex" @click="toggleExpand">
      <div class="building-id fw-bold pe-3">building id : {{building.id}}</div>

      <div class="expand-button ms-auto">
        {{ isExpanded ? '&#9660;' : '&#9658;' }}
      </div>
    </div>
    <template v-if="isExpanded">
      <hr/>
      <div class="rooms-list pt-3">
          <rooms-list-item 
          v-for="room in rooms"
          :room="room"
          :key="room.id"  
          >
          </rooms-list-item>
      </div>
    </template>
  </div>
</template>

<script>
import axios from 'axios';
import RoomsListItem from './RoomsListItem';


export default {
  components: { RoomsListItem },
  name: 'BuildingsListItem',
  props: ['building'],
  data: function() {
    return {
      isExpanded: false
    }
  }, 
  rooms: [],
  methods: {
    async toggleExpand() {
      let response = await axios.get(`https://farid-bechaalany.cleverapps.io/api/rooms/buildings/${this.building.id}`);
      let rooms = response.data;
      this.rooms=rooms;
      this.isExpanded = !this.isExpanded;
    }
  },
}
</script>

<style lang="scss" scoped>
  .top-row {
    cursor: pointer;
  }
</style>