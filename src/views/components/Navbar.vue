<template>
  <v-app-bar
    :clipped-left="$vuetify.breakpoint.lgAndUp"
    app
    color="blue darken-4"
    dark
  >
    <v-toolbar-title style="width: 300px" class="ml-0 pl-4">
      <span class="hidden-sm-and-down">Vysoké školy</span>
    </v-toolbar-title>

    <v-autocomplete
      v-model="autocomplete"
      @input="autocompleteSelected"
      :append-icon="null"
      label="Vyhledat školu, fakultu nebo obor"
      clearable
      :items="autocompleteOptions"
      flat
      solo-inverted
      prepend-inner-icon="search"
      no-data-text="Nic nenalezeno"
    >
      <template v-slot:item="{ index, item }">
        {{ item }}
        <div class="flex-grow-1"></div>
        <v-list-item-action @click.stop>
          <v-btn icon @click.stop.prevent="showChildren(item)">
            <v-icon>mdi-chevron-down</v-icon>
          </v-btn>
        </v-list-item-action>
      </template>
    </v-autocomplete>

    <div class="flex-grow-1"></div>
    <v-btn icon>
      <v-icon>mdi-information-outline</v-icon>
    </v-btn>
  </v-app-bar>
</template>

<script>
export default {
  name: "Navbar",
  props: {
    selected: Array
  },
  data: () => ({
    autocomplete: null,
    allOptions: [
      "Autocompletes",
      "Comboboxes",
      "Forms",
      "Inputs",
      "Overflow Buttons",
      "Selects",
      "Selection Controls",
      "Sliders",
      "Textareas",
      "Text Fields"
    ]
  }),

  methods: {
    showChildren(item) {
      console.log("Show children of ", item);
    },
    autocompleteSelected(value) {
      if (value) {
        this.$emit("select-option", value);
        this.$nextTick(() => {
          this.autocomplete = null;
        });
      }
    }
  },

  computed: {
    autocompleteOptions() {
      return this.allOptions.filter(item => {
        return !this.selected.includes(item);
      });
    }
  }
};
</script>