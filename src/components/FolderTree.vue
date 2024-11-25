<template>
    <ul class="folder-tree">
      <li v-for="folder in folders" :key="folder.id">
        <div @click="toggleFolder(folder.id)">
          <span v-if="folder.children.length">
            {{ isOpen(folder.id) ? '📂' : '📁' }}
          </span>
          <span @click.stop="selectFolder(folder.id)">
            {{ folder.name }}
          </span>
        </div>
        <folder-tree 
          v-if="isOpen(folder.id)" 
          :folders="folder.children" 
          @select="$emit('select', $event)"
        />
      </li>
    </ul>
  </template>
  
  <script lang="ts">
  import { defineComponent, ref } from 'vue';
  
  export interface Folder {
    id: number;
    name: string;
    children: Folder[];
  }
  
  export default defineComponent({
    name: 'FolderTree',
    props: {
      folders: {
        type: Array as () => Folder[],
        required: true,
      },
    },
    emits: ['select'],
    setup(_, { emit }) {
      const openFolders = ref<Set<number>>(new Set());
  
      const toggleFolder = (folderId: number) => {
        openFolders.value.has(folderId)
          ? openFolders.value.delete(folderId)
          : openFolders.value.add(folderId);
      };
  
      const isOpen = (folderId: number) => openFolders.value.has(folderId);
      const selectFolder = (folderId: number) => emit('select', folderId);
  
      return { toggleFolder, isOpen, selectFolder };
    },
  });
  </script>
  
  <style scoped>
  .folder-tree {
    list-style-type: none;
    padding-left: 20px;
  }
  .folder-tree > li {
    margin: 5px 0;
  }
  .folder-tree > li div {
    cursor: pointer;
  }
  </style>