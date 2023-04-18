<template>
    <div>
      <!-- Form to create new category -->
      <form @submit.prevent="addCategory">
        <label for="category-name">Category Name:</label>
        <input
          id="category-name"
          type="text"
          v-model="newCategoryName"
          placeholder="Enter category name"
        />
        <button type="submit">Create Category</button>
      </form>
  
      <!-- List of categories -->
      <ul>
        <li v-for="category in categories" :key="category.id">
          {{ category.name }}
          <button @click="deleteCategory(category.id)">Delete</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        categories: [], // Array to store categories
        newCategoryName: "", // Text input field to add new category
        nextCategoryId: 1 // Counter for assigning unique ids to new categories
      };
    },
  
    methods: {
      addCategory() {
        // Add new category to categories array
        this.categories.push({
          id: this.nextCategoryId++,
          name: this.newCategoryName
        });
  
        // Clear input field for new category name
        this.newCategoryName = "";
      },
  
      deleteCategory(categoryId) {
        // Remove category with matching id from categories array
        this.categories = this.categories.filter(
          category => category.id !== categoryId
        );
      }
    }
  };
  </script>
  