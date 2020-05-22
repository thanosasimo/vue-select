<template>
  <div id="app">
    <v-select v-model="selected" placeholder="Περιοχή" :multiple="true" label="label" :options="areas" :clearable="false">
      <template #selected-options="{selectedValue,getOptionLabel,getOptionKey,normalizeOptionForSlot,deselect,multiple,disabled,childComponents,scopeSearch}" v-if="selected">
        <template v-if="selectedValue.length<3">
          <span
            v-for="option in selectedValue"
            :key="getOptionKey(option)"
            :option="normalizeOptionForSlot(option)"
            :deselect="deselect"
            :multiple="multiple"
            :disabled="disabled"
            class="vs__selected"
          >
            {{option.label}}
            <button
              v-if="multiple"
              :disabled="disabled"
              type="button"
              class="vs__deselect"
              ref="deselectButtons"
              @click="deselect(option)"
            >
              <!-- :title="`Deselect ${getOptionLabel(option)}`" -->
              <!-- :aria-label="`Deselect ${getOptionLabel(option)}`" -->
              <component :is="childComponents.Deselect" />
            </button>
          </span>
          
          <input class="vs__search" v-bind="scopeSearch.attributes" v-on="scopeSearch.events">
        </template>
        <template v-else>
          <span>Multiple areas selected</span>
        </template>
      </template>
    </v-select>
  </div>
</template>

<script>
  import vSelect from "../src/components/Select";
  import countries from "../docs/.vuepress/data/countryCodes";
  import books from "../docs/.vuepress/data/books";

  export default {
    components: {
      vSelect
    },
    data: () => ({
      selected: null,
      areas: countries,
      // config: {
      //   options: areas
      // }
    })
  };
</script>

<style>
  html,
  body {
    margin: 0;
    height: 100%;
    font-family: -apple-system, sans-serif;
  }

  #app {
    height: 100%;
    max-width: 20rem;
    margin: 10rem auto 0;
  }

  hr {
    border: none;
    border-bottom: 1px solid #cacaca;
    margin-bottom: 1em;
    padding-top: 1em;
    width: 90%;
  }
</style>