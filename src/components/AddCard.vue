<template>
  <div class="">
    <button
      class="btn btn-sm btn-info w-100"
      v-if="!inAddMode"
      @click="inAddMode = true"
    >
      Add Card
    </button>

    <form
      action="#"
      class="card p-3"
      @submit.prevent="handleSubmit"
      @reset="handleReset"
      ref="form"
      v-else
    >
      <div class="form-group">
        <input
          type="text"
          name="title"
          id="title"
          class="form-control"
          placeholder="Something interesting..."
          v-model="cardData"
        />
      </div>
      <div class="d-flex justify-content-center">
        <button type="submit" class="btn w-50 btn-primary mr-3">Save</button>
        <button type="reset" class="btn w-50 btn-danger">
          Cancel
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inAddMode: false,
      cardData: '',
    };
  },
  methods: {
    handleSubmit() {
      if (this.cardData.trim()) {
        this.$emit('newcard', this.cardData.trim());
        this.cardData = '';
        this.inAddMode = false;
      }
    },
    handleReset() {
      this.cardData = '';
      this.inAddMode = false;
    },
  },
};
</script>

<style></style>
