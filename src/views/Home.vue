<template>
  <div class="home">
    <div class="btn-container">
      <UIButton
        @click="btnClick"
        :xsmall="xsmall"
        :small="small"
        :large="large"
        :xlarge="xlarge"
        :tile="tile"
        :rounded="rounded"
        :circle="circle"
        :disabled="disabled"
      ></UIButton>
      <div class="btn-group">
        <UIButton @click="resize('xsmall')">超小</UIButton>
        <UIButton @click="resize('small')">小</UIButton>
        <UIButton @click="resize('large')">大</UIButton>
        <UIButton @click="resize('xlarge')">超大</UIButton>
      </div>
      <div class="btn-group">
        <UIButton @click="changeRadius('tile')">矩形</UIButton>
        <UIButton @click="changeRadius('normal')">正常</UIButton>
        <UIButton @click="changeRadius('rounded')">圆角</UIButton>
        <UIButton @click="changeRadius('circle')">圆形</UIButton>
      </div>
      <div class="btn-group">
        <UIButton @click="changeDisabled">禁用</UIButton>
      </div>
    </div>
    {{books[1]}}
    {{books[2].one}}
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import UIButton from "../components/UIkit/UIButton.vue";

@Component({
  components: { UIButton }
})
export default class Home extends Vue {
  private books: any = [
    18,
    "aaa",
    {
      one: 1,
      two: 2
    }
  ];

  private xsmall: boolean = false;
  private small: boolean = false;
  private large: boolean = false;
  private xlarge: boolean = false;

  private tile: boolean = false;
  private rounded: boolean = false;
  private circle: boolean = false;

  private disabled: boolean = false;

  private btnClick() {
    console.log("btnClick");
  }

  private changeDisabled() {
    this.disabled = !this.disabled;
    this.books[1] = "bbb";
    this.books[2].one = 3;
  }

  private resize(size: string) {
    switch (size) {
      case "xsmall":
        this.xsmall = true;
        this.small = false;
        this.large = false;
        this.xlarge = false;
        break;
      case "small":
        this.xsmall = false;
        this.small = true;
        this.large = false;
        this.xlarge = false;
        break;
      case "large":
        this.xsmall = false;
        this.small = false;
        this.large = true;
        this.xlarge = false;
        break;
      case "xlarge":
        this.xsmall = false;
        this.small = false;
        this.large = false;
        this.xlarge = true;
        break;
    }
  }

  private changeRadius(radius: string) {
    switch (radius) {
      case "tile":
        this.tile = true;
        this.rounded = false;
        this.circle = false;
        break;
      case "normal":
        this.tile = false;
        this.rounded = false;
        this.circle = false;
        break;
      case "rounded":
        this.tile = false;
        this.rounded = true;
        this.circle = false;
        break;
      case "circle":
        this.tile = false;
        this.rounded = false;
        this.circle = true;
        break;
    }
  }
}
</script>

<style scoped lang="stylus">
.btn-group {
  display: flex;
  margin: 20px;
}
</style>