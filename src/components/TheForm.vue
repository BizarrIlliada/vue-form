<template>
  <form @submit.prevent="onSubmit">
    <div class="form-control" :class="{ invalid: usernameValidity === 'invalid' }">
      <label for="user-name">Your Name</label>
      <input
        id="user-name"
        name="user-name"
        type="text"
        v-model.trim="username"
        @blur="validateInput"
      />
      <p v-if="usernameValidity === 'invalid'">
        Please, enter a valid name!
      </p>
    </div>

    <div class="form-control">
      <label for="age">Your Age (Years)</label>
      <input id="age" name="age" type="number" v-model.number="age" ref="ageInput" />
    </div>

    <div class="form-control">
      <label for="referrer">How did you hear about us?</label>
      <select id="referrer" name="referrer" v-model="referrer">
        <option value="google">Google</option>
        <option value="wom">Word of mouth</option>
        <option value="newspaper">Newspaper</option>
      </select>
    </div>

    <div class="form-control">
      <h2>What are you interested in?</h2>
      <div>
        <input
        id="interest-news"
        value="news"
        name="interest"
        type="checkbox"
        v-model="interest"
        />
        <label for="interest-news">News</label>
      </div>
      <div>
        <input
        id="interest-tutorials"
        value="tutorials"
        name="interest"
        type="checkbox"
        v-model="interest"
        />
        <label for="interest-tutorials">Tutorials</label>
      </div>
      <div>
        <input
        id="interest-nothing"
        value="nothing"
        name="interest"
        type="checkbox"
        v-model="interest"
        />
        <label for="interest-nothing">Nothing</label>
      </div>
    </div>
    
    <div class="form-control">
      <h2>How do you learn?</h2>
      <div>
        <input
        id="how-video"
        value="video"
        name="how"
        type="radio"
        v-model="how"
        />
        <label for="how-video">Video Courses</label>
      </div>
      <div>
        <input
        id="how-blogs"
        value="blogs"
        name="how"
        type="radio"
        v-model="how"
        />
        <label for="how-blogs">Blogs</label>
      </div>
      <div>
        <input
        id="how-other"
        value="other"
        name="how"
        type="radio"
        v-model="how"
        />
        <label for="how-other">Other</label>
      </div>
    </div>
    
    <div class="form-control">
      <RatingControl v-model="rating" />
    </div>

    <div class="form-control">
      <input type="checkbox" id="confirm-terms" name="confirm-terms" v-model="confirm">
      <label for="confirm-terms">I agree with terms of use.</label>
    </div>
    
    <div>
      <button>Save Data</button>
    </div>
  </form>
</template>

<script>
  import RatingControl from './RatingControl.vue';

  export default {
    name: 'TheForm',
    components: { RatingControl },
    
    data() {
      return {
        username: '',
        age: null,
        referrer: 'wom',
        interest: [],
        how: null,
        confirm: false,
        usernameValidity: 'pending',
        rating: null,
      }
    },
    
    methods: {
      onSubmit() {
        console.log('Username: ', this.username);
        this.username = '';

        console.log('Age: ', this.age);
        this.age = null;

        console.log('Select: ', this.referrer);
        this.referrer = 'wom';

        console.log('Checkboxes: ', this.interest);
        this.interest = [];

        console.log('Radiobutton: ', this.how);
        this.how = null;

        console.log('Rating: ', this.rating);
        this.rating = null;

        console.log('Confirm: ', this.confirm);
        this.confirm = false;
      },

      validateInput() {
        // const { value } = event.target;
        // console.log('Value: ', value);
        if (!this.username) {
          this.usernameValidity = 'invalid';
        } else {
          this.usernameValidity = 'valid';
        }
      },
    }
  }
</script>

<style scoped>
  form {
    margin: 2rem auto;
    max-width: 40rem;
    border-radius: 12px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    padding: 2rem;
    background-color: #ffffff;
  }

  .form-control {
    margin: 0.5rem 0;
  }

  .form-control.invalid input {
    background-color: #f7d1d199;
    border: 1px solid red;
    border-radius: 2px;
  }

  .form-control.invalid label {
    color: red;
  }

  label {
    font-weight: bold;
  }

  h2 {
    font-size: 1rem;
    margin: 0.5rem 0;
  }

  input,
  select {
    display: block;
    width: 100%;
    font: inherit;
    margin-top: 0.5rem;
  }

  select {
    width: auto;
  }

  input[type='checkbox'],
  input[type='radio'] {
    display: inline-block;
    width: auto;
    margin-right: 1rem;
  }

  input[type='checkbox'] + label,
  input[type='radio'] + label {
    font-weight: normal;
  }

  button {
    font: inherit;
    border: 1px solid #0076bb;
    background-color: #0076bb;
    color: white;
    cursor: pointer;
    padding: 0.75rem 2rem;
    border-radius: 30px;
  }

  button:hover,
  button:active {
    border-color: #002350;
    background-color: #002350;
  }
</style>