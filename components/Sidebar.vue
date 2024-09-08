<template>
  <n-space vertical>
    <n-layout has-sider class="h-screen ">
      <n-layout-sider
        bordered
        class="bg-gray-700"
        collapse-mode="width"
        :collapsed-width="64"
        :width="240"
        :collapsed="collapsed"
        show-trigger
        @collapse="collapsed = true"
        @expand="collapsed = false"
      >
        <n-menu
          :collapsed="collapsed"
          :collapsed-width="64"
          :collapsed-icon-size="22"
          :options="menuOptions"
          :render-label="renderMenuLabel"
          :render-icon="renderMenuIcon"
          :expand-icon="expandIcon"
        />
      </n-layout-sider>
      <n-layout>
        <span>content</span>

      </n-layout>
    </n-layout>
  </n-space>
</template>
  
<script setup  >
import { defineComponent, h, ref } from 'vue'
import { NIcon, NSpace, NSwitch, NLayout, NLayoutSider, NMenu } from 'naive-ui'
import { BookmarkOutline, CaretDownOutline } from "@vicons/ionicons5";

const collapsed = ref(true)

const menuOptions = [
  {
    label: "Hear the Wind Sing",
    key: "hear-the-wind-sing",
    href: "https://en.wikipedia.org/wiki/Hear_the_Wind_Sing"
  },
  {
    label: "Pinball 1973",
    key: "pinball-1973",
    children: [
      {
        label: "Rat",
        key: "rat"
      }
    ]
  },
]


function renderMenuLabel(option) {
  if ("href" in option) {
    return h("a", { href: option.href, target: "_blank" }, [
      option.label
    ]);
  }
  return option.label;
}

function renderMenuIcon(option) {
  if (option.key === "sheep-man")
    return true;
  if (option.key === "food")
    return null;
  return h(NIcon, null, { default: () => h(BookmarkOutline) });
}

function expandIcon() {
  return h(NIcon, null, { default: () => h(CaretDownOutline) });
}

</script>
