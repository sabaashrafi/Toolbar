<template>
  <b-container>
    <b-row>
      <b-col cols="1">
        <!-- sidebar  -->
        <b-sidebar
          width="80px"
          class="bg-dark"
          no-close-on-esc
          v-model="showSidebar"
        >
          <b-form-group class="d-flex flex-column">
            <!-- handmode button  -->

            <b-icon
              v-shortkey="['esc']"
              @shortkey="handMode = !handMode"
              icon="hand-index"
              :class="[handMode ? 'hand-on' : 'hand-off']"
              @click="handMode = !handMode"
            >
            </b-icon>
            <!-- end handmode button  -->

            <hr />
            <!-- radio buttons in sidebar -->
            <b-form-radio-group label="Stacked " v-model="selected">
              <b-form-radio
                v-for="(item, index) in sidebarTools"
                :key="index"
                :name="item.name"
                :value="item.name"
                :disabled="!handMode"
              >
                <b-icon
                  v-shortkey="[item.shortKey]"
                  @shortkey="shortCutTool(item)"
                  :icon="item.icon"
                  @click="clickedTool(item)"
                  class="mt-2"
                  :class="[selected === item.name ? 'hand-on' : 'hand-off']"
                >
                </b-icon>
              </b-form-radio>
            </b-form-radio-group>
            <!-- end radio buttons in sidebar -->
          </b-form-group>
        </b-sidebar>
        <!-- end sidebar -->
      </b-col>
      <b-col cols="11">
        <p class="mt-5">{{ $t('handMode') }} : {{ handMode }}</p>
        <p>{{ $t('choosenTool') }} : {{ selected }}</p>
      </b-col>
    </b-row>
  </b-container>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'
// an interface for create custom tool type
interface sidebarTool {
  name: String
  icon: String
  shortKey: string
}
@Component({})
// @vuese
// a toolbar with hand mode and shortcut key
export default class IndexPage extends Vue {
  sidebarTools: Array<sidebarTool> = [
    { name: 'frame', icon: 'bounding-box', shortKey: '1' },
    { name: 'Brush', icon: 'brush', shortKey: '2' },
    { name: 'house', icon: 'house-door', shortKey: '3' },
    { name: 'pencil', icon: 'pencil', shortKey: '4' },
  ]
  selected: String = 'Brush'
  showSidebar: boolean = true
  handMode: boolean = true
  // methodas
  // @vuese
  //fire when shortcut tools clicked
  shortCutTool(item: sidebarTool) {
    this.selected = item.name
  }
  //fire when in handmode and tools clicked
  clickedTool(item: sidebarTool) {
    if (this.handMode) {
      this.selected = item.name
    }
  }
}
</script>

<style>
.hand-on {
  color: aquamarine;
}
.hand-off {
  color: #d5d8dc;
}
.b-sidebar {
  text-align: center;
  background-color: #2c3e50 !important;
}
hr {
  border-top: 1px solid rgba(255, 255, 255, 0.4);
}
.custom-radio .custom-control-label::before {
  display: none;
}
.custom-radio .custom-control-input:checked ~ .custom-control-label::after {
  display: none;
}
</style>
