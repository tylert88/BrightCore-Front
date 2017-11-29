<template>
  <div>
    <bright-core v-bind:features="features"></bright-core>
  </div>
</template>
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

<script>
import sweetalert from 'sweetalert';
import BrightCore from './components/brightCore';
import CreateFeature from './components/CreateFeature';

export default {
  name: 'app',
  components: {
    BrightCore,
    CreateFeature,
  },
  // data function avails data to the template
  data() {
    return {
      features: [{
        title: 'Todo A',
        project: 'Project A',
        done: false,
         },
        {
        title: 'Todo B',
        project: 'Project B',
        done: false,
      },
      {
        title: 'Todo C',
        project: 'Project C',
        done: false,
      }, {
        title: 'Todo D',
        project: 'Project D',
        done: false,
      }],
  };
  },
  methods: {
    createFeature(newFeature) {
      this.features.push(newFeature);
      sweetalert('Success!', 'To-Do created!', 'success');
    },
  },
};
</script>
