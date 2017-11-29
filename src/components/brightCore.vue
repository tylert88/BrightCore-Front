<template>
  <div>
    <p class="options">Added Features: {{features.filter(feature => {return feature.done === true}).length}}</p>
    <p class="options">Optional Features: {{features.filter(feature => {return feature.done === false}).length}}</p>
    <feature v-on:delete-feature="deleteFeature" v-on:complete-feature="completeFeature" v-for="feature in features" :feature.sync="feature"></feature>
  </div>
</template>

<script type = "text/javascript" >
import sweetalert from 'sweetalert';
import Feature from './Feature';

export default {
  props: ['features'],
  components: {
    Feature,
  },
  methods: {
    deleteFeature(feature) {
      sweetalert(
        {
          title: 'Are you sure?',
          text: 'This Feature will be permanently deleted!',
          type: 'warning',
          showCancelButton: true,
          confirmButtonColor: '#DD6B55',
          confirmButtonText: 'Yes, delete it!',
          closeOnConfirm: false,
        },
        () => {
          const featureIndex = this.features.indexOf(feature);
          this.features.splice(featureIndex, 1);
          sweetalert('Deleted!', 'Your Feature has been deleted.', 'success');
        },
      );
    },
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
