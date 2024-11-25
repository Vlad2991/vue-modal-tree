<script lang="ts">
import { ref } from 'vue';
import AppButton from '@/components/AppButton.vue';
import Modal from '@/components/Modal.vue';
import FolderTree from '@/components/FolderTree.vue';

export default {
  components: { AppButton, Modal, FolderTree },
  setup() {
    const isModalOpen = ref(false);
    const folders = ref([
      { id: 1, name: 'Папка 1', children: [
          { id: 2, name: 'Папка 1.1', children: [] },
          { id: 3, name: 'Папка 1.2', children: [
              { id: 4, name: 'Папка 1.2.1', children: [] },
          ]},
        ]},
      { id: 5, name: 'Папка 2', children: [] },
    ]);
    const selectedFolder = ref<number | null>(null);

    const openModal = () => (isModalOpen.value = true);
    const closeModal = () => (isModalOpen.value = false);
    const handleSelect = (folderId: number) => {
      selectedFolder.value = folderId;
      closeModal();
      alert(`Вы выбрали папку с ID: ${folderId}`);
    };
    const selectFolder = (folderId: number) => (selectedFolder.value = folderId);

    return { isModalOpen, folders, openModal, closeModal, handleSelect, selectFolder };
  },
};

</script>

<template>
  <div id="app">
    <app-button @click="openModal">Открыть</app-button>
    <modal 
      v-if="isModalOpen" 
      title="Выберите папку" 
      @close="closeModal" 
      @select="handleSelect"
    >
      <folder-tree 
        :folders="folders" 
        @select="selectFolder" 
      />
    </modal>
  </div>
 
</template>

<style scoped>
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

</style>
