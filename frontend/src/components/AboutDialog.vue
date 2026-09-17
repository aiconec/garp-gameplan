<template>
  <Dialog v-model:open="show" size="sm" bare>
    <div class="p-4 pt-5">
      <div class="flex justify-center">
        <div class="flex flex-col items-center">
          <GameplanLogo class="mb-3 size-12" />
          <h3 class="text-3xl-semibold text-ink-gray-9">GARP Spaces</h3>
          <div class="flex items-center mt-1">
            <div class="text-base text-ink-gray-6">
              {{ appVersion.branch != 'main' ? appVersion.branch : '' }}
              <template v-if="appVersion.branch != 'main'"> ({{ appVersion.commit }}) </template>
              <template v-else>{{ appVersion.tag }}</template>
            </div>

            <Tooltip :text="`${appVersion.commit_message} - ${appVersion.commit_date}`" side="top">
              <span class="lucide-info size-3.5 text-ink-gray-8 ml-1" />
            </Tooltip>
          </div>
        </div>
      </div>
      <hr class="border-t my-3 mx-2" />
      <div>
        <a
          v-for="link in links"
          :key="link.label"
          class="flex py-2 px-2 hover:bg-surface-gray-1 rounded-4 cursor-pointer"
          target="_blank"
          :href="link.url"
        >
          <GithubLogo v-if="link.icon === 'github'" class="size-4 mr-2 text-ink-gray-7" />
          <span v-else-if="link.icon" :class="[link.icon, 'size-4 mr-2 text-ink-gray-7']" />
          <span class="text-base text-ink-gray-8">
            {{ link.label }}
          </span>
        </a>
      </div>
      <hr class="border-t my-3 mx-2" />
      <p class="text-sm text-ink-gray-6 px-2 mt-2">
        <!-- Upstream copyright, licence and no-warranty notices live on the
             licences page; this link is how the dialog displays them. -->
        © AICONEC and contributors ·
        <a
          href="https://garp.aiconec.com/docs/licences"
          target="_blank"
          class="underline underline-offset-2 hover:text-ink-gray-8"
        >
          Licences
        </a>
      </p>
    </div>
  </Dialog>
</template>
<script setup lang="ts">
import { Tooltip } from 'frappe-ui'
import GameplanLogo from './GameplanLogo.vue'
import GithubLogo from './GithubLogo.vue'
let show = defineModel<boolean>()

let links = [
  {
    label: 'Website',
    url: 'https://aiconec.com',
    icon: 'lucide-globe',
  },
  {
    label: 'Documentation',
    url: 'https://garp.aiconec.com/docs/modules/projects',
    icon: 'lucide-book-open',
  },
  {
    label: 'Contact Support',
    url: 'https://aiconec.com/support',
    icon: 'lucide-headset',
  },
]

interface AppVersion {
  branch: string
  commit: string
  commit_date: string
  commit_message: string
  tag?: string
}
let appVersion: AppVersion = window.app_version
</script>
