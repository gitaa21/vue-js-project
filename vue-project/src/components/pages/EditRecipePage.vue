<template>
    <main>
        <div class="container-md my-5 py-5">
            <recipe-form v-if="detailData && !isLoading" :isEdit="true"></recipe-form>
        </div>
    </main>
</template>

<script setup>
import RecipeForm from '../recipeForm/RecipeForm.vue';
import { useStore } from 'vuex';
import { useRoute } from 'vue-router';
import { onMounted, ref } from 'vue';


const store = useStore()
const route = useRoute()
const detailData = ref()
let isLoading = false

onMounted(async () => {
    try {
        isLoading = true
        await store.dispatch(
            "recipe/getRecipeDetail", route.params.id
        )
        detailData.value = store.state.recipe.recipeDetail;
        isLoading = false
    } catch (error) {
        console.log(error);
    }
})


</script>