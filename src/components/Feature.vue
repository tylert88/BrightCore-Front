<template>
  <div class='ui centered card'>
    <div class="content" v-show="!isEditing">
      <div class='header'>
          {{ feature.title }}
      </div>
      <div class='meta'>
          {{ feature.project }}
      </div>
      <div class='extra content'>
          <span class='right floated edit icon' v-on:click="showForm">
          <i class='edit icon'></i>
        </span>
        <span class='right floated trash icon' v-on:click="deleteFeature(feature)">
          <i class='trash icon'></i>
        </span>
      </div>
    </div>
    <div class="content" v-show="isEditing">
      <div class='ui form'>
        <div class='field'>
          <label>Title</label>
          <input type='text' v-model="feature.title" >
        </div>
        <div class='field'>
          <label>Project</label>
          <input type='text' v-model="feature.project" >
        </div>
        <div class='ui two button attached buttons'>
          <button class='ui basic blue button' v-on:click="hideForm">
            Close X
          </button>
        </div>
      </div>
    </div>
    <div class='ui bottom attached green basic button' v-show="!isEditing &&feature.done" disabled>
        Added
    </div>
    <div class='ui bottom attached blue basic button' v-on:click="completeFeature(feature)" v-show="!isEditing && !feature.done">
        Add this feature
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
    deleteFeature(feature) {
      this.$emit('delete-feature', feature);
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
