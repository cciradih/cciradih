<script setup>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faBilibili, faGithub } from '@fortawesome/free-brands-svg-icons'
import { faEnvelope } from '@fortawesome/free-solid-svg-icons'
import { ref, onMounted } from 'vue'
const issues = ref([])
onMounted(async () => {
  const issuesApi = 'https://api.github.com/repos/cciradih/issues/issues?state=open&creator=cciradih&per_page=5'
  const response = await fetch(issuesApi)
  const json = await response.json()
  issues.value = json
})
const readMore = '阅读更多'
const links = [
  {
    url: 'https://space.bilibili.com/2078718',
    icon: faBilibili
  },
  {
    url: 'https://github.com/cciradih',
    icon: faGithub
  },
  {
    url: 'mailto:trash@cciradih.eu.org',
    icon: faEnvelope
  }
]
const tools = [
  {
    link: 'https://vuejs.org/',
    title: 'Powered by Vue.js'
  },
  {
    link: 'https://tailwindcss.com/',
    title: 'Designed by Tailwind CSS'
  },
]
const copyrights = [
  {
    link: 'https://www.gnu.org/licenses/gpl-3.0-standalone.html',
    title: 'GPLv3'
  },
  {
    link: 'https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh',
    title: 'BY-NC-SA 4.0'
  },
  {
    link: 'https://cciradih.eu.org',
    title: '@ 2016 - ' + new Date().getFullYear() + ' Cciradih & Heartless.'
  }
]
const username = 'Cciradih'
const title = 'Full Stack Developer'
const issuesUrl = 'https://github.com/cciradih/cciradih/issues'
</script>

<template>
  <div class="w-screen h-screen flex justify-center items-center bg-[#0f1011] text-[#ffffff] select-none">
    <div class="w-11/12 xl:w-1/2 h-full flex flex-col justify-center items-center gap-8 lg:gap-16">
      <div class="w-full pt-8 lg:pt-16 flex justify-center items-center gap-8 lg:gap-16">
        <a :href="link.url" target="_blank" v-for="link in links">
          <FontAwesomeIcon
            class="text-2xl lg:text-3xl text-[#e3e4e6] hover:text-[#4f52b4] transition-text duration-300 ease-in-out delay-0"
            :icon="link.icon" />
        </a>
      </div>
      <div
        class="relative w-full flex-1 rounded before:absolute before:inset-1 before:rounded before:bg-[#0f1011] before:z-10 after:absolute after:w-[300%] after:h-[300%] after:-top-full after:-left-full after:bg-[conic-gradient(#0f1011,#5e69d1,#0f1011)] after:animate-spin overflow-hidden">
        <div class="relative w-full h-full flex flex-col lg:flex-row justify-center items-center z-20">
          <div class="w-full h-1/2 lg:w-1/2 lg:h-full p-1">
            <div class="w-full h-full p-1 flex flex-col justify-center items-center gap-1.5 lg:gap-2 bg-[#232326]">
              <div class="text-4xl lg:text-5xl font-serif">{{ username }}</div>
              <div class="text-xl lg:text-2xl font-mono font-light text-[#e3e4e6]">{{ title }}</div>
            </div>
          </div>
          <div class="w-full h-1/2 lg:w-1/2 lg:h-full p-1">
            <div class="w-full h-full p-1 flex flex-col text-[#e3e4e6] overflow-auto">
              <div class="w-full flex-1 flex flex-col justify-center items-center gap-2">
                <div class="w-full flex flex-col justify-start items-start rounded" v-for="issue in issues">
                  <a class=" px-2 py-1 rounded lg:text-lg line-clamp-1 text-[#7281ff] hover:text-[#4f52b4] transition-text duration-300 ease-in-out delay-0"
                    target="_blank" :href="issue.html_url">{{ issue.title }}</a>
                </div>
              </div>
              <a class="p-2 lg:p-4 self-end lg:text-lg text-[#e3e4e6] hover:text-[#4f52b4] transition-text duration-300 ease-in-out delay-0"
                target="_blank" :href="issuesUrl">{{ readMore }}</a>
            </div>
          </div>
        </div>
      </div>
      <div
        class="w-full pb-8 lg:pb-16 flex flex-col justify-center items-center gap-3 text-sm lg:text-base text-[#969799]">
        <div class="flex flex-col md:flex-row justify-center items-center md:divide-x md:divide-[#969799]">
          <a class="px-2 hover:text-[#4f52b4] transition-text duration-300 ease-in-out delay-0" target="_blank"
            :href="tool.link" v-for="(tool, index) in tools" :key="index">{{ tool.title }}</a>
        </div>
        <div class="flex flex-col md:flex-row justify-center items-center md:divide-x md:divide-[#969799]">
          <a class="px-2 hover:text-[#4f52b4] transition-text duration-300 ease-in-out delay-0" target="_blank"
            :href="copyright.link" v-for="(copyright, index) in copyrights" :key="index">{{ copyright.title }}</a>
        </div>
      </div>
    </div>
  </div>
</template>
