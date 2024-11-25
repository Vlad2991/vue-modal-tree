<template>
    <div class="modal-backdrop" @click.self="$emit('close')">
      <div class="modal">
        <h3>{{ title }}</h3>
        <div class="modal-content">
          <slot />
        </div>
        <div class="modal-actions">
          <app-button @click="$emit('close')">Закрыть</app-button>
          <app-button @click="emitSelection">Ок</app-button>
        </div>
      </div>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, ref } from 'vue';
  import AppButton from './AppButton.vue';
  
  export default defineComponent({
    name: 'Modal',
    components: { AppButton },
    props: {
      title: {
        type: String,
        required: true,
      },
    },
    emits: ['close', 'select'],
    setup(_, { emit }) {
      const selectedFolder = ref<number | null>(null);
  
      const emitSelection = () => {
        if (selectedFolder.value !== null) {
          emit('select', selectedFolder.value);
        }
      };
  
      return { selectedFolder, emitSelection };
    },
  });
  </script>
  
  <style scoped>
  .modal-backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .modal {
    background: white;
    padding: 20px;
    border-radius: 8px;
    width: 400px;
  }
  .modal-actions {
    display: flex;
    justify-content: space-between;
    margin-top: 20px;
  }
  </style>