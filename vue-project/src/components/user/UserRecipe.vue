<template>
  <ul class="list-group">
    <li class="list-group-item">
      <div class="d-flex flex-sm-row flex-column justify-content-between align-items-sm-center">
        <div class="mb-3 mb-sm-0">
          <p class="my-0 fs-4 fw-semibold">My Recipe</p>
          <p class="my-0 text-secondary">Add your original recipe here</p>
        </div>
        <div>
          <router-link to="/new-recipe" class="btn add-btn px-3 py-2 rounded-pill">
            <i class="fa-solid fa-circle-plus pe-2"></i>Add Recipe
          </router-link>
        </div>
      </div>
    </li>
    <li class="list-group-item">
      <p class="mt-2 mb-4 fs-5 fw-semibold">Recipe</p>
      <div class="row">
        <user-recipe-card v-for="recipe in recipeList" :key="recipe.id" :recipe="recipe"
          :buttonName="['Delete', 'Edit']" @btnRemove="deleteRecipe(recipe.id)" @btnEdit="editRecipe(recipe.id)">
          <p>{{ new Date(recipe.createAt).toDateString() }}</p>
        </user-recipe-card>
      </div>
    </li>
  </ul>
</template>

<script setup>
import UserRecipeCard from './UserRecipeCard.vue';
import { computed, onMounted, ref } from 'vue';
import { createLogger, useStore } from 'vuex';
import { useRouter } from 'vue-router';

const router = useRouter();
const store = useStore();

const recipeList = ref();

const recipes = computed(() => {
  const allRecipe = store.state.recipe.recipes;
  const userId = store.state.auth.userLogin.userId;
  return allRecipe.filter((recipe) => recipe.userId === userId);
})

const editRecipe = (id) => {
  const uid = isNaN(Number(id))

  router.push({ name: 'editRecipePage', params: { id: uid ? `${id}` : id } });
};

const deleteRecipe = async (id) => {
  await store.dispatch("recipe/deleteRecipe", id)
  alert("Data Berhasil di Hapus")
}

onMounted(async () => {
  try {
    await store.dispatch("recipe/getRecipeData");
    recipeList.value = store.state.recipe.recipes;
    console.log(recipeList)
  } catch (error) {
    console.log(error);
  }
})




</script>