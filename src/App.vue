<script setup>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { faBilibili, faGithub } from '@fortawesome/free-brands-svg-icons'
import { faEnvelope } from '@fortawesome/free-solid-svg-icons'
import { ref } from 'vue'
const issues = ref([])
const url = 'https://api.github.com/repos/cciradih/issues/issues?state=open&creator=cciradih&per_page=5'
fetch(url)
  .then(repsonse => repsonse.json())
  .then(json => issues.value = json)
const links = ref([
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
])
const tools = ref([
  {
    link: 'https://vuejs.org/',
    title: 'Powered by Vue.js'
  },
  {
    link: 'https://tailwindcss.com/',
    title: 'Designed by Tailwind CSS'
  },
])
const copyrights = ref([
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
    title: '@ 2023 - ' + new Date().getFullYear() + ' Cciradih.eu.org & Heartless.'
  }
])
</script>

<template>
  <div class="w-screen h-screen flex justify-center items-center bg-[#0f1011] text-[#ffffff] select-none">
    <div class="w-11/12 lg:w-1/2 h-full flex flex-col justify-center items-center gap-8 lg:gap-16">
      <div class="w-full flex justify-center gap-12">
        <a :href="link.url" target="_blank" v-for="link in links">
          <FontAwesomeIcon
            class="text-2xl lg:text-3xl text-[#e3e4e6] hover:text-[#7281ff] hover:cursor-pointer transition-text duration-300 ease-in-out delay-0"
            :icon="link.icon" />
        </a>
      </div>
      <div
        class="w-full h-2/3 lg:h-1/2 flex flex-col lg:flex-row justify-center items-center border border-[#23252a] rounded bg-[#161618]">
        <div class="w-full h-1/2 lg:w-1/2 lg:h-full flex flex-col justify-center items-center gap-1.5 lg:gap-2">
          <div class="text-4xl lg:text-5xl font-serif">Cciradih</div>
          <div class="text-xl lg:text-2xl font-mono font-light text-[#e3e4e6]">Full Stack Developer</div>
        </div>
        <div class="w-full h-1/2 lg:w-1/2 lg:h-full p-2 flex flex-col bg-[#1c1c1f] text-[#e3e4e6]">
          <div class="w-full flex-1 flex flex-col justify-center items-center gap-2">
            <div class="w-full flex flex-col justify-start items-start rounded hover:bg-[#e3e4e6]" v-for="issue in issues">
              <a class="w-full px-2 py-1 border border-[#23252a] rounded lg:text-lg line-clamp-1 hover:text-[#7281ff] hover:cursor-pointer transition-text duration-300 ease-in-out delay-0"
                target="_blank" :href="issue.html_url">{{ issue.title }}</a>
            </div>
          </div>
          <a class="self-end lg:text-lg hover:text-[#7281ff] hover:cursor-pointer transition-text duration-300 ease-in-out delay-0"
            target="_blank" href="https://github.com/cciradih/cciradih/issues">
            阅读更多</a>
        </div>
      </div>
      <div class="w-full flex flex-col justify-center items-center gap-3 text-sm lg:text-base text-[#969799]">
        <div class="flex flex-col md:flex-row justify-center items-center md:divide-x md:divide-[#969799]">
          <a class="px-2 hover:text-[#7281ff] transition-text duration-300 ease-in-out delay-0" target="_blank"
            :href="tool.link" v-for="(tool, index) in tools" :key="index">{{ tool.title
            }}</a>
        </div>
        <div class="flex flex-col md:flex-row justify-center items-center md:divide-x md:divide-[#969799]">
          <a class="px-2 hover:text-[#7281ff] transition-text duration-300 ease-in-out delay-0" target="_blank"
            :href="copyright.link" v-for="(copyright, index) in copyrights" :key="index">{{
          copyright.title }}</a>
        </div>
      </div>
    </div>
  </div>
</template>
