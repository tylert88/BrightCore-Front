<template>
  <div class='ui centered card'>
    <div class="content">

      <div class='ui form' v-model="feature.type">
        <div class='field'>
        <label>Risk Policy Features:</label>
        </div>

        <div class='field'>
          <label>Custom Feature</label>
          <input type='text' v-model="feature.name" placeholder="Full Coverage" >
        </div>

        <div class='field'>
          <label>Custom Feature</label>
          <input type='text' v-model="feature.value" placeholder="$5000">
        </div>

        <div class='field'>
          <label>Custom Feature</label>
          <input type='text' v-model="feature.type" placeholder="Months">
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
export default {
  props: ['feature'],
  data() {
    return {
      isEditing: false,
    };
  },
  methods: {
    completeFeature(feature) {
      this.$emit('complete-feature', feature);
    },
    showForm() {
      this.isEditing = true;
    },
    hideForm() {
      this.isEditing = false;
    },
  },
};
</script>
