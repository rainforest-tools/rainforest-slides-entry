<template lang="pug">
.full.flex-center
  .card.glass.flex(class="lg:card-side")
    figure.p-4
      img.full.object-cover(:src="img" style="max-width: 50vw")
    .card-body.flex-shrink
      ul.menu.collapse.collapse-arrow.collapse-open
        template(:key="key" v-for="[key, value] of Object.entries(structure)")
          li.menu-title.collapse-title
            .flex.items-center
              FolderOpenIcon.h-8.w-8.pr-2
              p {{key}}
          .collapse-content
            li(:key="`${key}_${title}`" v-for="[title, path] of Object.entries(value)")
              template(v-if="'subPages' in path && Object.keys(path.subPages).length > 0")
                a
                  FolderOpenIcon.h-8.w-8.pr-2
                  p {{ title }}
                ul.menu
                  li(:key="`${key}_${title}_${subPageTitle}`" v-for="[subPageTitle, subPage] of Object.entries(path.subPages)")
                    a(:href="`/${path.path}/${subPage.path}`" target="_blank" @mouseover="img=`/previews/${path.path}/${subPage.path}/01.png`") {{ subPageTitle }}
              a(:href="`/${path.path}`" target="_blank" v-else @mouseover="img=`/previews/${path.path}/01.png`") {{ title }}
</template>
<script setup lang="ts">
import { ref } from "vue"
import { FolderIcon, FolderOpenIcon } from '@heroicons/vue/outline'
import structure from "@/assets/structure.json"
const img = ref<string>("")
</script>
