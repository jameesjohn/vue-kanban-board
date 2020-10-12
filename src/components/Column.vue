<template>
  <div class="col-md-3 card column" ref="column">
    <header class="card-header">
      <h3 class="col">{{ column.name }}</h3>
      <AddCard @newcard="$emit('newcard', $event)"></AddCard>
    </header>
    <div class="card-list">
      <Card v-for="(card, index) in column.cards" :key="index" :card="card" />
    </div>
  </div>
</template>

<script>
import Card, { CardDataType } from './Card';
import AddCard from './AddCard';
export default {
  name: 'Column',
  components: {
    Card,
    AddCard,
  },
  props: {
    column: {
      type: Object,
      required: true,
    },
  },
  mounted() {
    this.enableDrop();
  },

  methods: {
    enableDrop() {
      const column = this.$refs.column;
      column.addEventListener('dragenter', this.handleDragEnter);
      column.addEventListener('dragover', this.handleDragOver);
      column.addEventListener('drop', this.handleDrop);
    },

    /**
     * @param {DragEvent} event
     */
    handleDragEnter(event) {
      if (event.dataTransfer.types.includes[CardDataType]) {
        // Only handle dragging cards.
        event.preventDefault();
      }
    },

    handleDragOver(event) {
      // Create a move effect.
      event.dataTransfer.dropEffect = 'move';
      event.preventDefault();
    },

    /**
     * @param {DragEvent} event
     */
    handleDrop(event) {
      const data = event.dataTransfer.getData(CardDataType);
      // Emit a card moved event.
      this.$emit('cardMoved', data);
    },
  },
};
</script>

<style scoped>
div.column {
  padding: 0;
  padding-bottom: 15px;
  margin: 0 15px;
  box-shadow: 0 0 10px #cccccc;
}
div.card-list {
  padding: 0 15px;
}
header {
  margin-bottom: 10px;
}
header h3 {
  text-align: center;
}
</style>
