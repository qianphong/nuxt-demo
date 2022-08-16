<script setup lang='ts'>
const props = withDefaults(defineProps<{ name: string; nameModifiers: { capitalize: boolean } }>(), { name: '1', nameModifiers() { return { capitalize: false } } })
const emit = defineEmits<{ (e: 'update:name', name: string): void }>()
const { count, inc, dec } = useCount()

const computedName = computed({
  get() {
    return props.name
  },
  set(name: string) {
    emit('update:name', props.nameModifiers.capitalize ? name.charAt(0).toUpperCase() + name.slice(1) : name)
  },
})
</script>

<template>
  <div><input v-model="computedName" type="text"></div>
  <div inline-flex m="y-3">
    <button btn p-2 rounded-full @click="dec()">
      <div i-carbon-subtract />
    </button>
    <div font="mono" w="15" m-auto inline-block>
      {{ count }}
    </div>
    <button btn p-2 rounded-full @click="inc()">
      <div i-carbon-add />
    </button>
  </div>
</template>
