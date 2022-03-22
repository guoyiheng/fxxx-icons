<script setup lang="ts">

// type
interface IconType {
  type: string
  list: IconMeta[]
}
interface IconMeta {
  iconUrl: string
  keyword: ''
  color: ''
}

// icon list
const defaultIcons = ref([
  {
    type: 'Wandering',
    list: [
      {
        iconUrl: 'https://api.iconify.design/icon-park:video-two.svg?color=%23888888',
        keyword: 'video',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/fluent:movies-and-tv-20-filled.svg?color=%23888888',
        keyword: 'movie',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/icon-park:book.svg?color=%23888888',
        keyword: 'book',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/flat-color-icons:idea.svg?color=%23888888',
        keyword: 'idea',
        color: '',
      },
      {
        iconUrl: 'https://s3.bmp.ovh/imgs/2022/03/5e1221f27dd912e6.png',
        keyword: 'game',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/icon-park:music-one.svg?color=%23888888',
        keyword: 'musci',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/icon-park:write.svg?color=%23888888',
        keyword: 'note',
        color: '',
      },
    ],

  },
  {
    type: 'Technology',
    list: [
      {
        iconUrl: 'https://api.iconify.design/logos:javascript.svg?color=%23888888',
        keyword: 'javascript',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/mdi:github.svg?color=%23888888',
        keyword: 'github',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/vscode-icons:file-type-git.svg?color=%23888888',
        keyword: 'git',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/vscode-icons:file-type-vue.svg?color=%23888888',
        keyword: 'vue',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/vscode-icons:file-type-vite.svg?color=%23888888',
        keyword: 'vite',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/ri:macbook-fill.svg?color=%23888888',
        keyword: 'pc',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/wpf:mac-os.svg?color=%23888888',
        keyword: 'apple',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/mdi:language-markdown.svg?color=%23888888',
        keyword: '',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/vscode-icons:file-type-light-pnpm.svg?color=%23888888',
        keyword: '',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/logos:npm-icon.svg?color=%23888888',
        keyword: '',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/ic:baseline-http.svg?color=%23888888',
        keyword: '',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/ion:paper-airplane.svg?color=%23888888',
        keyword: '',
        color: '',
      },

      {
        iconUrl: 'https://api.iconify.design/vscode-icons:file-type-css.svg?color=%23888888',
        keyword: '',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/vscode-icons:file-type-reactjs.svg?color=%23888888',
        keyword: '',
        color: '',
      },
      {
        iconUrl: 'https://api.iconify.design/vscode-icons:file-type-vscode.svg?color=%23888888',
        keyword: '',
        color: '',
      },
    ],
  },

])
const customizeIcons = useStorage<IconType>('customize-icon', {
  type: 'Customize',
  list: [],
})
const iconList = computed(() => {
  return [...defaultIcons.value, customizeIcons.value]
})

// copy and remove
const clipboard = useClipboard()
function handleCopyUrl(iconUrl: string) {
  clipboard.copy(iconUrl)
}
function handleRemoveUrl(index: number) {
  customizeIcons.value.list.splice(index, 1)
}

// add icon
const iconUrl = ref('')
function addIcon() {
  const icon: IconMeta = {
    iconUrl: iconUrl.value,
    keyword: '',
    color: '',
  }
  customizeIcons.value.list.push(icon)
  iconUrl.value = ''
}
function getIconName(url: string) {
  const iconName = url.split('/')[url.split('/').length - 1]
  return iconName.split('.')[0]
}

</script>

<template>
  <div sm:w-50vw w-full m-auto>
    <h1 text-size-8 mb-6>
      Fine icons for Notion
    </h1>
    <div v-for="iconType in iconList" :key="iconType.type" mb-4>
      <h2 mb-4>
        {{ iconType.type }}
      </h2>
      <ul>
        <li
          v-for="(iconObj,index) in iconType.list" :key="iconObj.iconUrl"
          flex items-center justify-center gap-4
          mb-2
        >
          <img :src="iconObj.iconUrl" alt="" w-16px h-16px>
          <div w-60 truncate>
            {{ getIconName(iconObj.iconUrl ) }}
          </div>
          <button class="btn" @click="handleCopyUrl(iconObj.iconUrl)">
            copy
          </button>
          <button
            v-if="iconType.type === 'Customize'"
            class="btn-warning"
            @click="handleRemoveUrl(index)"
          >
            remove
          </button>
        </li>
      </ul>
    </div>
    <div mb-4>
      <div flex items-center justify-center gap-2>
        <input
          v-model="iconUrl"
          type="text"
          placeholder="Icon url"
          autocomplete="false"
          outline-none
          border="1 base"
          text="center"
          bg="transparent"
          @keydown.enter="addIcon"
        >
        <button class="btn" @click="addIcon">
          Add
        </button>
      </div>
    </div>
  </div>
</template>
