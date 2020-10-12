<template>
  <div class="card" ref="card">
    <div class="card-body">{{ card.value }}</div>
  </div>
</template>

<script>
export const CardDataType = 'text/x-kanban-card';

export default {
  name: 'Card',
  props: {
    card: {
      type: Object,
      required: true,
    },
  },

  mounted() {
    this.setDraggable();
  },

  methods: {
    setDraggable() {
      // Get Card element.
      const card = this.$refs.card;
      card.draggable = true;

      // Setup event listeners.
      card.addEventListener('dragstart', this.handleDragStart);
      card.addEventListener('dragend', this.handleDragEnd);
    },

    /**
     * @param {DragEvent} event
     */
    handleDragStart(event) {
      const dataTransfer = event.dataTransfer;
      // Set the data to the value of the card which is gotten from props.
      dataTransfer.setData(CardDataType, this.card.value);
      dataTransfer.effectAllowed = 'move';

      // Add visual cues to show that the card is no longer in it's position.
      event.target.style.opacity = 0.2;
    },

    handleDragEnd(event) {
      // Return the opacity to normal when the card is dropped.
      event.target.style.opacity = 1;
    },
  },
};
</script>

<style scoped>
div.card {
  margin-bottom: 15px;
  box-shadow: 0 0 5px #cccccc;
  transition: all ease 300ms;
  background: #fdfdfd;
}
div.card:hover {
  box-shadow: 0 0 10px #aaaaaa;
  background: #ffffff;
}
</style>
