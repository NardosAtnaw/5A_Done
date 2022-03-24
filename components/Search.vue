<template>
    <!-- <ais-instant-search :search-client="searchClient" index-name="docs">
      <ais-configure
        :attributesToSnippet="['bodyPlainText']"
        :hits-per-page.camel="5"
      >
        <ais-autocomplete>
          <div slot-scope="{ currentRefinement, indices, refine }">
            <input type="search" ref="searchInput"   placeholder="Search..." class="w-full py-2 px-3" :value="currentRefinement"
            @input="refine($event.currentTarget.value)" 
            autocomplete="off"/>
            <div
              v-show="currentRefinement.length"
              class="absolute z-10 transform mt-3 px-2 w-screen max-w-md sm:px-0"
            >
              <div
                class="rounded-Lg shadow-Lg ring-1 ring-black ring-opacity-5 overflow-hidden"
              >
                <div
                  class="relative grid gap-6 bg-gray-908 text-gray-100 px-5 py-6 sm:gap-8 sm:p-8"
                >
                <div v-if="currentRefinement">

                  <div v-for="section in indices"
                    :key="section.objectID"
                    class="divide-y divide-blue-900"
                  >
                    <div v-if="section.hits.length">
                      <h2 class="uppercase text-orange-500 py-1 px-2">
                        {{ section.indexName }}
                      </h2>
                    </div>
                    <a to="#" v-for="(hit) in section.hits" :key="hit.objectID "
                      class="block text-sm col-span-2 py-2 transition ease-in-out duration-150"
                    >
                      <div class="px-2">
                        <ais-highlight
                          attribute="title"
                          :hit="hit"
                          class="block text-blue-300 font-medium"
                        />
                        <ais-snippet
                          attribute="bodyPlainText"
                          :hit="hit"
                          class="block text-gray-108 font-base"
                        />
                      </div>
                    </a>
                  </div>
                </div>
                  <ais-powered-by theme="dark" class="px-2" />
                </div>
              </div>
            </div>
          </div>
        </ais-autocomplete>
      </ais-configure>
    </ais-instant-search> -->
      <ais-instant-search :search-client="searchClient" index-name="instant_search">
    <ais-search-box />
    <ais-stats />
    <ais-refinement-list attribute="brand" />
    <ais-hits>
      <template v-slot:item="{ item }">
        <p>
          <ais-highlight attribute="name" :hit="item" />
        </p>
        <p>
          <ais-highlight attribute="brand" :hit="item" />
        </p>
      </template>
    </ais-hits>
    <ais-pagination />
  </ais-instant-search>
</template>

<script>
// import algoliasearch from 'algoliasearch/lite';
// import 'instantsearch.css/themes/satellite-min.css'

// const searchClient = algoliasearch(
//   'RMY5TWV3Y0',
//   'b45ce43f158ccbb1c4d309d2f1522ce8'
// )
// export default {
// data() {
//     return {
//      searchClient,
//     };
//   },
// }
import {
  AisInstantSearch,
  AisRefinementList,
  AisHits,
  AisHighlight,
  AisSearchBox,
  AisStats,
  AisPagination,
  createServerRootMixin,
} from 'vue-instantsearch';
import algoliasearch from 'algoliasearch/lite';

const searchClient = algoliasearch(
  'latency',
  'b45ce43f158ccbb1c4d309d2f1522ce8'
);

export default {
  components: {
    AisInstantSearch,
    AisRefinementList,
    AisHits,
    AisHighlight,
    AisSearchBox,
    AisStats,
    AisPagination,
  },
  data() {
    return {
      searchClient,
    };
  },
  head() {
    return {
      link: [
        {
          rel: 'stylesheet',
          href: '<%= app_data.cdn.instantsearch_css_satellite.url %>',
        },
      ],
    };
  },
};
</script>

<style>

</style>