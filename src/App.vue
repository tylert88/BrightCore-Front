<template>
  <div id="app">

    <div class='ui three column centered grid'>
      <div class='column'>
        <create-feature v-on:create-feature="createFeature"></create-feature>
        <brite-core v-bind:features="features"></brite-core>
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
import sweetalert from 'sweetalert';
import BriteCore from './components/BriteCore';
import CreateFeature from './components/CreateFeature';

export default {
  name: 'app',
  components: {
    BriteCore,
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
