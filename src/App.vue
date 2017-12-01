<template>
  <div id="app">

    <div class='ui three column centered grid'>
      <div class='column'>
        <create-feature v-on:create-feature="createFeature"></create-feature>
        <bright-core v-bind:features="features"></bright-core>
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
import sweetalert from 'sweetalert';
import BrightCore from './components/brightCore';
import CreateFeature from './components/CreateFeature';

export default {
  name: 'app',
  components: {
    BrightCore,
    CreateFeature,
  },
  data() {
    return {
      features: [],
    };
  },
  methods: {
    createFeature(newFeature) {
      this.features.push(newFeature);
      sweetalert('Success!', 'Policy Risk created!', 'success');
    },
  },
};
</script>
