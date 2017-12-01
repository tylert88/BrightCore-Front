<template>
  <div class='ui basic content center aligned segment'>
    <button class='ui basic button blue icon' v-on:click="openForm" v-show="!isCreating">
      Add Policy
      <i class='plus icon green'></i>
    </button>
    <div class='ui centered card' v-show="isCreating">
      <div class='content'>
        <div class='ui form'>
          <div class='field'>
            <select v-model="policy.type">
              <option  v-for="option in options"  v-bind:value="option.value">
                {{ option.text }}
              </option>
            </select>
            <br>
            <span>Risk Selected: <strong>{{ policy.type }}</strong></span>
          </div>
          <div class='field' v-show="policy.type && policy.type.length > 1">
            <label for="">Customer Name</label>
            <input v-model="policy.name" type="text" name="customer" placeholder="Bill Murray" required>
            </div>
          <div class='field' v-show="policy.type && policy.type.length > 1">
            <label v-show="policy.type == 'Automobile'" >Make / Model</label>
            <label v-show="policy.type == 'Home'">Address</label>
            <label v-show="policy.type == 'Life'">Policy Holder</label>
            <label v-show="policy.type == 'Prize'">Company Name</label>
            <input v-model="policy.policyType" type="text" name="customer" required>
          </div>
          <div class='field' v-show="policy.type && policy.type.length > 1">
            <label for="">Item Value</label>
            <input v-model="policy.amount" type="number" name="value" placeholder="$5000" required>
            </div>
          <div class='field' v-show="policy.type && policy.type.length > 1">
            <label for="">Effective date</label>
            <input v-model="policy.expires" type="date" name="date" v-on:change="addFeature()" required>
            </div>
          <div class="field" >
            <button class='ui basic blue button' v-show="policy.type" v-on:click="addFeature()" >
              Add Features
              <i class='plus icon blue'></i>
            </button>
          </div>
          <feature  v-for="feature in policy.features" key="feature.id" :feature.sync="feature"></feature>
          <div class='ui two button buttons'>
            <button class='ui basic green button' v-on:click="sendForm()" >
            <i class='check icon green'></i>
          </button>
          <button class='ui basic red button' v-on:click="closeForm">
            <i class='x icon red'></i>
          </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import sweetalert from 'sweetalert';
import Feature from './Feature';

export default {
  components: {
    Feature,
  },
  data() {
    return {
      policy: {
        features: [],
      },
      isCreating: false,
      selected: '',
      options: [],
    };
  },
  mounted() {
    this.apiCall();
  },

  methods: {
    completeFeature(feature) {
      this.$emit('complete-feature', feature);
    },
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.isCreating = false;
    },
    addFeature() {
      this.policy.features.push({ name: '', value: '' });
    },
    apiCall() {
      this.$http.get(process.env.API_URL).then(res => {
        const data = res.data.objects.map(el => ({ text: el.policy_type, value: el.policy_type }));
        this.options = data;
        console.log(data);
      });
    },
    sendForm() {
      if (this.policy.name && this.policy.policyType && this.policy.amount && this.policy.expires) {
        this.closeForm();
        sweetalert('Success!', 'Policy Risk Added!', 'success');
      }
    },
  },
};
</script>
