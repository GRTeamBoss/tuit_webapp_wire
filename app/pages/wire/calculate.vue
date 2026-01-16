<template>
  <UPageSection>
    <UPageHero title="Calculate" />
    <USelectMenu
      v-model="categoryDefault"
      :items="categories"
      @update:model-value="changeCables($event)"
    />
    <USelectMenu v-model="cableDefault" :items="cablesByCategory" />
    <UPageCard :title="cableDefault">
      <template #footer>
        <p class="text-green-400">
          {{ cableDesc }}
        </p>
      </template>
    </UPageCard>
  </UPageSection>
</template>

<script setup lang="ts">
const categories = ref(["Ethernet", "MMF", "SMF", "Data Center"]);
const categoryDefault = ref("Ethernet");
const cableDefault = ref("Cat5e");
const cablesByCategory = ref(["Cat5e", "Cat6", "Cat6a", "Cat7", "Cat8"]);
const cables = ref([
  {
    Ethernet: [
      {
        name: "Cat5e",
        type: "twisted_pair",
        distance: "100 m",
        speed: "1 Gbps",
      },
      {
        name: "Cat6",
        type: "twisted_pair",
        distance: "100 m (1G), 55 m (10G)",
        speed: "1 Gbps / 10 Gbps",
      },
      {
        name: "Cat6a",
        type: "twisted_pair",
        distance: "100 m",
        speed: "10 Gbps",
      },
      {
        name: "Cat7",
        type: "shielded_twisted_pair",
        distance: "100 m",
        speed: "10 Gbps",
      },
      {
        name: "Cat8",
        type: "shielded_twisted_pair",
        distance: "30 m",
        speed: "25–40 Gbps",
      },
    ],
    MMF: [
      {
        name: "OM2",
        type: "multimode_fiber",
        distance: "550 m",
        speed: "1 Gbps",
      },
      {
        name: "OM3",
        type: "multimode_fiber",
        distance: "300 m",
        speed: "10 Gbps",
      },
      {
        name: "OM4",
        type: "multimode_fiber",
        distance: "400 m",
        speed: "10 Gbps",
      },
      {
        name: "OM5",
        type: "multimode_fiber",
        distance: "150 m",
        speed: "40–100 Gbps",
      },
    ],
    SMF: [
      {
        name: "OS2 (G.652D)",
        type: "singlemode_fiber",
        distance: "10 km",
        speed: "1–10 Gbps",
      },
      {
        name: "OS2 (10GBASE-LR)",
        type: "singlemode_fiber",
        distance: "10 km",
        speed: "10 Gbps",
      },
      {
        name: "OS2 (40GBASE-LR4)",
        type: "singlemode_fiber",
        distance: "10 km",
        speed: "40 Gbps",
      },
      {
        name: "OS2 (100GBASE-LR4)",
        type: "singlemode_fiber",
        distance: "10 km",
        speed: "100 Gbps",
      },
      {
        name: "OS2 (DWDM)",
        type: "singlemode_fiber",
        distance: "40–80 km",
        speed: "100–400 Gbps",
      },
    ],
    "Data Center": [
      {
        name: "DAC (Passive)",
        type: "copper_dac",
        distance: "1–3 m",
        speed: "10–40 Gbps",
      },
      {
        name: "DAC (Active)",
        type: "copper_dac",
        distance: "5–7 m",
        speed: "10–40 Gbps",
      },
      {
        name: "AOC",
        type: "active_optical_cable",
        distance: "10–100 m",
        speed: "10–100 Gbps",
      },
    ],
  },
]);
const cableDesc = ref(
  `type: ${
    cables.value[0][categoryDefault.value].filter((cable) => {
      if (cable.name === cableDefault.value) {
        return cable;
      }
    })[0].type
  } - distance: ${
    cables.value[0][categoryDefault.value].filter((cable) => {
      if (cable.name === cableDefault.value) {
        return cable;
      }
    })[0].distance
  } - speed: ${
    cables.value[0][categoryDefault.value].filter((cable) => {
      if (cable.name === cableDefault.value) {
        return cable;
      }
    })[0].speed
  }`
);

const changeCables = (category: string) => {
  cableDefault.value = cables.value[0][category][0].name;
  cablesByCategory.value = [];
  cables.value[0][category].forEach((cable) => {
    cablesByCategory.value.push(cable.name);
  });
  cableDesc.value = `type: ${
    cables.value[0][categoryDefault.value].filter((cable) => {
      if (cable.name === cableDefault.value) {
        return cable;
      }
    })[0].type
  } - distance: ${
    cables.value[0][categoryDefault.value].filter((cable) => {
      if (cable.name === cableDefault.value) {
        return cable;
      }
    })[0].distance
  } - speed: ${
    cables.value[0][categoryDefault.value].filter((cable) => {
      if (cable.name === cableDefault.value) {
        return cable;
      }
    })[0].speed
  }`;
};
</script>
