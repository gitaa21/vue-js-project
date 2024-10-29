<template>
    <ul class="list-group">
        <recipe-form-header></recipe-form-header>
        <recipe-form-body :isEdit="isEdit"></recipe-form-body>
    </ul>
</template>

<script setup>
defineProps({
  isEdit: {
    type: Boolean,
    default: false
  }
})

import RecipeFormHeader from './RecipeFormHeader.vue';
import RecipeFormBody from './RecipeFormBody.vue';

</script>