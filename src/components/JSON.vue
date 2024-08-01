<!-- JSONLab.vue -->
<template>
  <div class="json-lab">
    <h1>🗄️ JSON Data & Vue Directives Lab</h1>

    <section class="lab-section">
      <h2>📚 Working with JSON Arrays</h2>
      <p>Our <code>authors.json</code> contains an array of author objects.</p>

      <h3>Iterating through Arrays</h3>
      <!-- Activity 6: Render a list containing author names and their birth years. Hint: Make use of the v-for directive to iterate through the array of authors. -->
      <!-- TODO: CODE TO RENDER LIST OF AUTHORS HERE -->
      <ul>
        <li v-for="author in authors" :key="author.id">
          {{ author.name }} ({{ author.birthYear }})
        </li>
      </ul>

      <h3>Filtering Arrays</h3>
      <!-- Activity 7: Render a list containing authors born after 1850. Hint: Make use of the v-for directive to iterate through the array of authors that you have filtered out. -->
      <p>Authors born after 1850:</p>
      <!-- TODO: CODE TO RENDER LIST OF AUTHORS HERE -->
      <ul>
        <li v-for="modernAuthor in modernAuthors" :key="modernAuthor.id">
          {{ modernAuthor.name }} ({{ modernAuthor.birthYear }})
        </li>
      </ul>

      <h3>Mapping Arrays</h3>
      <p>Famous works:</p>
      <ul>
        <!-- Activity 8: Render a list of all famous works. Hint: Use the v-for directive to iterate through the array of authors that you have filtered out. -->
        <!-- TODO: CODE TO RENDER LIST OF FAMOUS WORKS HERE -->
        <li v-for="work in allFamousWorks" :key="work">
          {{ work }}
        </li>
      </ul>

      <h3>Finding in Arrays</h3>
      <p>Finding by property: {{ orwellName }}</p>

      <h3>Nested Arrays/Objects</h3>
      <p>{{ austenName }}'s works:</p>
      <!-- Activity 9: Render a list of Austen's works. Hint: Use the v-for directive to iterate through the array of authors that you have filtered out. -->
      <!-- TODO: CODE TO RENDER LIST OF AUSTEN'S WORKS HERE -->

      <ul>
        <li v-for="work in austenWorks" :key="work.title">
          {{ work.title }} ({{ work.year }})
        </li>
      </ul>
    </section>

    <section class="lab-section">
      <h2>🏢 Working with JSON Objects</h2>
      <p>Our <code>bookstores.json</code> is a JSON object.</p>

      <h3>Accessing Properties</h3>
      <p>
        Company:
        <!-- Activity 9a: Get the company name from the bookstores object. -->
        <!-- TODO: CODE TO GET COMPANY NAME HERE -->
        <b>{{ companyName }}</b>
      </p>

      <p>
        Total Stores:
        <!-- Activity 9b: Get the total number of stores from the bookstores object. -->
        <!-- TODO: CODE TO GET TOTAL STORES HERE -->
        <b>{{ totalStores }}</b>
      </p>

      <h3>Iterating Object Properties</h3>
      <p>Store Types:</p>
      <!-- Activity 10: Iterate through the storeTypes array and display the store type and the number of stores that use that type. -->
      <!-- TODO: CODE TO RENDER LIST OF STORE TYPES HERE -->
      <ul>
        <li v-for="(count, type) in storeTypes" :key="type">
          {{ type }}: {{ count }} stores
        </li>
      </ul>

      <h3>Nested Objects</h3>
      <p>Opening Hours:</p>
      <!-- Activity 11: Iterate through the openingHours object and display the day of the week and the opening and closing times. -->
      <!-- TODO: CODE TO RENDER LIST OF OPENING HOURS HERE -->
      <ul>
        <li v-for="(hours, day) in openingHours" :key="day">
          {{ day }}: Open at {{ hours.open }}, Close at {{ hours.close }}
        </li>
      </ul>

      <h3>Working with Arrays in Objects</h3>
      <!-- Activity 12: Get the top sellers from the bookstores object. -->
      <!-- TODO: CODE TO GET TOP SELLERS HERE -->
      
      <p>We operate in:</p>
      <p>Our #1 seller:{{topSellersString}}</p>
    </section>

    <section class="lab-section">
      <h2>v-if & v-else</h2>
      <p>Toggle visibility based on a condition.</p>
      <!-- Activity 13: Toggle the message visibility when the button is clicked. -->
      <!-- TODO: CODE TO TOGGLE MESSAGE VISIBILITY HERE. Hint: Use the v-if directive. -->
      <button @click="showMessage = !showMessage">Toggle Message</button>
      <p v-if="showMessage" class="message success">✨ You're a Vue superstar! ✨</p>
      <p>Click the button to see a message.</p>
    </section>

    <section class="lab-section">
      <h2>Attribute, Class and Style Binding with <code>v-bind</code></h2>
      <p>Highlighting Specific Authors:<br>Jiayuan Feng<br>29289513</p>

    </section>
  </div>
</template>

<script setup>
import { ref, computed } from "vue"
import authors from "../assets/json/authors.json"
import bookstores from "../assets/json/bookstores.json"

// Activity 1: Import JSON files (authors.json and bookstores.json)
// TODO: CODE TO IMPORT JSON FILES HERE

const showMessage = ref(false)

// Activity 2: Get authors born after 1850
const modernAuthors = computed(() =>
  authors.filter((author) => author.birthYear > 1850)
);

// Activity 3: Get all famous works
const allFamousWorks = computed(() =>
  authors.flatMap((author) => author.famousWorks.map((work) => work.title))
);

// Activity 4: Find author by name
// const orwell = computed(() => {
//   return authors.value.find((author) => author.name === "George Orwell");
// });
const authorsData = ref(authors);
const orwell = computed(() => {
  return authorsData.value.filter((author) => author.name === "George Orwell");
});
const orwellName = computed(() => {
  return orwell.value.length > 0 ? orwell.value[0].name : 'Not found';
});


// Activity 5: Find author by ID
const austen = computed(() => {
  // TODO: CODE TO FIND AUTHOR BY ID HERE
  return authors.filter((author) => author.id === 1)
})
const austenName = computed(() => {
  return austen.value.length > 0 ? austen.value[0].name : 'Not found';
});
const austenWorks = computed(() => {
  return austen.value.length > 0 ? austen.value[0].famousWorks : 'Not found';
});

// bookstore data:
const bookstoresData = ref(bookstores);


const companyName = computed(() => bookstoresData.value.name);
const totalStores = computed(() => bookstoresData.value.totalStores);
const storeTypes = computed(() => bookstoresData.value.storeTypes);
const openingHours = computed(() => bookstoresData.value.openingHours);
const topSellersString = computed(() => {
      return bookstoresData.value && bookstoresData.value.topSellers
        ? bookstoresData.value.topSellers.join(', ')
        : 'No top sellers available.';
    });


</script>

<style scoped>
.json-lab {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  max-width: 80vw;
  margin: 0 auto;
  padding: 20px;
  background-color: #f4f4f4;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

h1,
h2 {
  color: #333;
}

h1 {
  text-align: center;
}

.lab-section {
  background-color: white;
  padding: 20px;
  margin-bottom: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.message {
  padding: 10px;
  border-radius: 5px;
  margin-top: 10px;
}

.success {
  background-color: #e7faf3;
  color: #42b883;
  border: 1px solid #42b883;
}

.highlight {
  background-color: #42b883;
}

code {
  background-color: #e0e0e0;
  padding: 2px 5px;
  border-radius: 4px;
  font-family: "Courier New", Courier, monospace;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  background-color: #f0f0f0;
  padding: 10px;
  margin: 5px 0;
  border-radius: 5px;
}
</style>
