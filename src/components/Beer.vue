<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12"></v-col>

      <v-col class="mb-4">
        <v-data-table :headers="headers" :items="beers" :items-per-page="5" class="elevation-1"></v-data-table>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
function getPagedURL(page) {
  return `https://api.punkapi.com/v2/beers?malt=Extra_Pale&page=${page}&per_page=80`;
}

function getBeers(page = 1, beers = []) {
  return fetch(getPagedURL(page))
    .then(response => response.json())
    .then(function(newBeers) {
      const allBeers = [...beers, ...newBeers];

      if (newBeers.length === 80) {
        page++;

        return getBeers(page, allBeers);
      }

      return allBeers;
    });
}

export default {
  data() {
    return {
      headers: [],
      beers: []
    };
  },
  created() {
    this.init();
  },
  methods: {
    init: function() {
      getBeers().then(fetchedBeers => {
        this.headers = Object.keys(fetchedBeers[0])
          .filter(
            key =>
              ![
                "id",
                "first_brewed",
                "abv",
                "ibu",
                "image_url",
                "target_fg",
                "target_og",
                "ebc",
                "srm",
                "ph",
                "attenuation_level",
                "boil_volume",
                "method",
                "volume",
                "ingredients",
                "brewers_tips",
                "contributed_by"
              ].includes(key)
          )
          .map(key => ({
            text: key,
            value: key
          }));

        this.beers = fetchedBeers;
      });
    }
  }
};
</script>
