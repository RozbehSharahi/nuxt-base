<template>
  <div>
    <div ref="grid" class="the-grid" :style="spaceFix">
      <slot />
    </div>
  </div>
</template>
<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  props: {
    spacingX: {
      type: Number,
      default: 20,
    },
    spacingY: {
      type: Number,
      default: 20,
    },
    unit: {
      type: String,
      default: 'px',
    },
  },
  computed: {
    spaceFix(): { [key: string]: string } {
      return {
        marginLeft: `${-this.spacingX / 2}${this.unit}`,
        marginRight: `${-this.spacingX / 2}${this.unit}`,
        marginTop: `${-this.spacingY / 2}${this.unit}`,
        marginBottom: `${-this.spacingY / 2}${this.unit}`,
      }
    },
  },
  watch: {
    spacingX(): void {
      this.setSpacesOnChildren()
    },
    spacingY(): void {
      this.setSpacesOnChildren()
    },
  },
  mounted(): void {
    this.setSpacesOnChildren()
  },
  methods: {
    setSpacesOnChildren(): void {
      // @ts-ignore
      const children: HTMLElement[] = Array.from(this.$refs.grid.children)
      for (const child of children) {
        child.style.paddingLeft = `${this.spacingX / 2}${this.unit}`
        child.style.paddingRight = `${this.spacingX / 2}${this.unit}`
        child.style.paddingTop = `${this.spacingY / 2}${this.unit}`
        child.style.paddingBottom = `${this.spacingY / 2}${this.unit}`
      }
    },
  },
})
</script>
<style lang="scss" scoped>
.the-grid {
  display: flex;
  flex-wrap: wrap;

  > * {
    width: 100%;
  }
}
</style>
