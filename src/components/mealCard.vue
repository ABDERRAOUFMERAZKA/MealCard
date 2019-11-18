<template>
  <form
    id="app"
    @submit.prevent="search"
  >
    <p v-if="errors.length">
      <b>Please correct the following error(s):</b>
      <ul>
        <li v-for="error in errors"  :key="error">{{ error }}</li>
      </ul>
    </p>

    <p>
      <label for="name">Meal name</label>
      <input
        id="name"
        v-model="name"
        type="text"
        name="name"
      >
    </p>
    <p>
     <input type="submit" />
    </p>
    <div v-if="meals.length" class="meals">
      <div v-for="(meal, index) of meals" :key="index">
        <div v-checkVegetarian="meal.strCategory" class="meal">
            <div>{{ meal.strMeal }}</div>
            <img v-bind:src="meal.strMealThumb" height="400" width="400" />
        </div>
        </div>
    </div>
  </form>
</template>
<script>
import axios from 'axios'
export default {
  name: 'CardMeal',
  data() {
    return {
      meals: [],
      errors: [],
      name: null,
    };
  },
  directives: {
  checkVegetarian: {
    // directive definition
    inserted: function (el, binding) {
      if (binding.value === 'Vegetarian') {
          el.style.borderColor = 'green';
      }
    }
  }
},
  methods:{
    search: function (e) {
      if (this.name) {
       axios.get("https://www.themealdb.com/api/json/v1/1/search.php?s="+this.name)
       .then(response => this.meals = response.data.meals)
       // eslint-disable-next-line
       .catch(e => console.error(e))
      }

      this.errors = [];

      if (!this.name) {
        this.errors.push('Name required.');
      }

      e.preventDefault();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.meals {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  flex-wrap: wrap;
}
.meal {
  border: 1px solid;
  display: flex;
  flex-direction: column;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
