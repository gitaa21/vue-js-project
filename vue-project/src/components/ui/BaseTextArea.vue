<template>
    <div>
        <label :for="identity" class="fw-semibold">{{ label }}
            <span style="color: #cb3a32;">*</span>
        </label>
        <textarea class="form-control" :id="identity" @keyup="$emit('update:modelValue', $event.target.value)" v-text="modelValue"></textarea>
    </div>
</template>

<script setup>
defineProps ({
    identity: {type: String, required: true},
    label: {type: String, required: true},
    placehorder: {type: String, required: true},
    modelValue: {type: String}
});

let emit = defineEmits(['update: modelValue'])

</script>