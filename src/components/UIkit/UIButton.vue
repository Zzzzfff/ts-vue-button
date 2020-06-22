<template>
  <div @click="onClickBtn">
    <button
      class="ui-button"
      :class="{
        'ui-btn-xsmall': xsmall,
        'ui-btn-small': small,
        'ui-btn-large': large,
        'ui-btn-xlarge': xlarge,
        'ui-btn-tile': tile,
        'ui-btn-rounded': rounded,
        'ui-btn-circle': circle,
        'ui-btn-disabled': disabled
      }"
      :style="`--color-tint: ${TintColor}`"
    >
      <slot>按钮</slot>
    </button>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue, Emit } from "vue-property-decorator";

@Component
export default class UIButton extends Vue {
  @Prop(Boolean) private xsmall!: boolean;
  @Prop(Boolean) private small!: boolean;
  @Prop(Boolean) private large!: boolean;
  @Prop(Boolean) private xlarge!: boolean;
  @Prop(Boolean) private tile!: boolean;
  @Prop(Boolean) private rounded!: boolean;
  @Prop(Boolean) private circle!: boolean;
  @Prop(Boolean) private disabled!: boolean;
  @Prop(String) public color: string | undefined;

  @Emit("click") private btnClick(event: MouseEvent) {}

  private get TintColor() {
    if (this.color) {
      return this.color;
    } else {
      return "#2D8CF0";
    }
  }

  private onClickBtn(event: MouseEvent) {
    if (!this.disabled) {
      this.btnClick(event);
    }
  }
}
</script>

<style scoped lang="stylus">
resize(minWidth, height, paddingLR, fontSize) {
  min-width: minWidth;
  height: height;
  padding: 0 paddingLR;
  font-size: fontSize;

  &.ui-btn-rounded, &.ui-btn-circle {
    border-radius: (@height / 2);
  }

  &.ui-btn-circle {
    width: @height;
    // 如果是圆，min-width和padding设置为0
    min-width: 0;
    padding: 0;
  }
}

.ui-button {
  resize(64px, 36px, 16px, 0.875rem);
  border: 0 solid black;
  border-radius: 6px;
  color: @17233D;
  background-color: var(--color-tint);
  font-weight: 500;
  letter-spacing: 0.09em;
  outline: none;
  cursor: pointer;
  user-select: none;

  &:hover {
    filter: brightness(120%);
  }

  &:active {
    filter: brightness(80%);
  }

  &.ui-btn-xsmall {
    resize(36px, 20px, 9px, 0.625rem);
  }

  &.ui-btn-small {
    resize(50px, 28px, 12px, 0.75rem);
  }

  &.ui-btn-large {
    resize(78px, 44px, 19px, 0.875rem);
  }

  &.ui-btn-xlarge {
    resize(92px, 52px, 23px, 1rem);
  }

  &.ui-btn-tile {
    border-radius: 0;
  }

  &.ui-btn-disabled {
    background-color: #F5F5F5;
    color: #C5C8CE;
    cursor: not-allowed;
  }
}
</style>