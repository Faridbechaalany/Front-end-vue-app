<template>
  <div class="window border border-secondary rounded p-2 mb-2" :class="{expanded: isExpanded}">
    <div class="top-row d-flex" @click="toggleExpand">
      <div class="window-name fw-bold pe-3">{{room.name}}</div>
      <div class="room-name text-muted">floor number : {{room.floor}}</div>

      <div class="expand-button ms-auto">
        {{ isExpanded ? '&#9660;' : '&#9658;' }}
      </div>
    </div>
    <template v-if="isExpanded">
      <hr/>
      <div class="windows-list pt-3">
          <windows-list-item 
          v-for="window in windows"
          :window="window"
          :key="window.id"  
          @window-updated="updateWindow"
          @window-deleted="updateList"
          >
          </windows-list-item>
      </div>
    </template>
  </div>
</template>

<script>
import axios from 'axios';
import WindowsListItem from './WindowsListItem';

export default {
  components: { WindowsListItem },
  name: 'RoomsListItem',
  props: ['room'],
  data: function() {
    return {
      isExpanded: false
    }
  }, 
  windows: [],
  methods: {
    async toggleExpand() {
      let response = await axios.get(`https://farid-bechaalany.cleverapps.io/api/windows/rooms/${this.room.id}`);
      let windows = response.data;
      this.windows=windows;
      this.isExpanded = !this.isExpanded;
    },
    updateWindow(newWindow) {
      let index = this.windows.findIndex(window => window.id === newWindow.id);
      this.windows.splice(index, 1, newWindow);
      this.isExpanded = !this.isExpanded;
      this.isExpanded = !this.isExpanded;
    },
    async updateList(){
      let response = await axios.get(`https://farid-bechaalany.cleverapps.io/api/windows/rooms/${this.room.id}`);
      let windows = response.data;
      this.windows=windows;
      this.isExpanded = !this.isExpanded;
      this.isExpanded = !this.isExpanded;
    }
  }
}
</script>

<style lang="scss" scoped>
  .top-row {
    cursor: pointer;
  }
</style>