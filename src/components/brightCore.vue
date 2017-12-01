<template>
  <div>
  </div>
</template>

<script>
import sweetalert from 'sweetalert';
import Feature from './Feature';

export default {
  props: ['features'],
  components: {
    Feature,
  },
  methods: {
    completeFeature(feature) {
      const featureIndex = this.features.indexOf(feature);
      this.features[featureIndex].done = true;
      sweetalert('Success!', 'Feature Added!', 'success');
    },
  },
};
</script>

<style scoped>
  p.options {
    text-align: center;
  }
</style>
