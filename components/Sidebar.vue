<template>
  <div :class="['h-screen w-64 flex flex-col', darkMode ? 'bg-gray-900 text-gray-400' : 'bg-gray-100 text-gray-700']">
    <div :class="['flex items-center justify-center h-14', darkMode ? 'text-white' : 'text-black']">
      <Icon :icon="'logos:nuxt-icon'" class="w-5 h-5 mr-2" />
      <span class="font-bold">Nuxt</span>
    </div>
    <div class="px-2">
      <div class="flex items-center my-1">
        <Icon :icon="'mdi:search-web'" :class="darkMode ? 'text-gray-400' : 'text-gray-700'" class="w-4 h-4" />
        <input
          :class="['ml-2 w-full rounded py-1 px-2 focus:outline-none text-sm', darkMode ? 'bg-gray-800 text-gray-300' : 'bg-gray-200 text-gray-700']"
          type="text"
          placeholder="Search..."
        />
      </div>
      <ul class="my-1 space-y-1">
        <li :class="menuItemClass">
          <Icon :icon="'mdi:home'" :class="iconClass" class="w-4 h-4" />
          <span class="ml-2 text-sm">Home</span>
        </li>
        <li :class="menuItemClass">
          <Icon :icon="'mdi:inbox'" :class="iconClass" class="w-4 h-4" />
          <span class="ml-2 text-sm">Inbox</span>
          <span :class="['ml-auto rounded-full px-2 text-xs', darkMode ? 'bg-gray-700 text-gray-300' : 'bg-gray-300 text-gray-600']">4</span>
        </li>
        <li :class="menuItemClass">
          <Icon :icon="'mdi:account'" :class="iconClass" class="w-4 h-4" />
          <span class="ml-2 text-sm">Users</span>
        </li>
      </ul>
      
      <!-- Dropdown Menu -->
      <input type="checkbox" id="settings-toggle" class="hidden peer" />
      <label :for="'settings-toggle'" :class="['flex items-center py-1 rounded cursor-pointer', darkMode ? 'hover:bg-gray-700' : 'hover:bg-gray-300']">
        <Icon :icon="'mdi:cog'" :class="iconClass" class="w-4 h-4" />
        <span class="ml-2 text-sm">Settings</span>
        <Icon :icon="'mdi:chevron-down'" :class="['ml-auto w-4 h-4 transition-transform duration-300', darkMode ? 'text-gray-400' : 'text-gray-700', 'peer-checked:rotate-180']" />
      </label>
      
      <ul :class="['ml-4 space-y-1 overflow-hidden transition-all duration-300 max-h-0 peer-checked:max-h-40', darkMode ? 'text-gray-400' : 'text-gray-700']">
        <li :class="menuItemClass">
          <div :class="['w-1 h-full', darkMode ? 'bg-gray-700' : 'bg-gray-400']"></div>
          <span class="ml-2 text-sm">General</span>
        </li>
        <li :class="menuItemClass">
          <div :class="['w-1 h-full', darkMode ? 'bg-gray-700' : 'bg-gray-400']"></div>
          <span class="ml-2 text-sm">Members</span>
        </li>
        <li :class="menuItemClass">
          <div :class="['w-1 h-full', darkMode ? 'bg-gray-700' : 'bg-gray-400']"></div>
          <span class="ml-2 text-sm">Notifications</span>
        </li>
      </ul>

      <ul>
        <li :class="['mt-2 text-xs', darkMode ? 'text-gray-500' : 'text-gray-600']">Colors</li>
        <li class="ml-2">
          <ul class="space-y-1">
            <li v-for="color in colors" :key="color" :class="menuItemClass">
              <span :class="`w-2.5 h-2.5 rounded-full bg-${color}-500`"></span>
              <span class="ml-2 text-sm capitalize">{{ color }}</span>
            </li>
          </ul>
        </li>
      </ul>
    </div>
    <div class="mt-auto mb-2 px-2">
      <ul class="space-y-1">
        <li :class="menuItemClass">
          <Icon :icon="'mdi:account-plus'" :class="iconClass" class="w-4 h-4" />
          <span class="ml-2 text-sm">Invite people</span>
        </li>
        <li :class="menuItemClass">
          <Icon :icon="'mdi:help-circle'" :class="iconClass" class="w-4 h-4" />
          <span class="ml-2 text-sm">Help & Support</span>
        </li>
        <li :class="menuItemClass">
          <img class="w-7 h-7 rounded-full" src="https://via.placeholder.com/40" alt="Profile Picture" />
          <span class="ml-2 text-sm">Benjamin</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { Icon } from '@iconify/vue';

// Dark mode state
const colorMode = useColorMode()
const darkMode = computed({
  get () {
    return colorMode.value === 'dark'
  },
  set () {
    colorMode.preference = colorMode.value === 'dark' ? 'light' : 'dark'
  }
});

// Class binding for dark/light mode
const menuItemClass = computed(() =>
  darkMode.value
    ? 'flex items-center py-1 hover:bg-gray-700 rounded'
    : 'flex items-center py-1 hover:bg-gray-300 rounded'
);

const iconClass = computed(() =>
  darkMode.value ? 'text-gray-400' : 'text-gray-700'
);

const colors = ['green', 'teal', 'cyan', 'sky', 'blue', 'indigo', 'violet'];
</script>

<style scoped>
/* Transition and toggle effect for the dropdown menu */
#settings-toggle:checked + label + ul {
  max-height: 100px; /* Adjust this value based on the content's height */
}

#settings-toggle:checked + label .mdi-chevron-down {
  transform: rotate(180deg);
}
</style>
