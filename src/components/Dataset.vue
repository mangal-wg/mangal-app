<template>
  <div>
    <v-container class="text-md-left">
      <div class="title teal--text">Informations</div>
      <v-divider class="pb-2"></v-divider>
      <div v-if="getDataset">
        <div>
          <span class="font-weight-bold body-2">Mangal dataset ID:</span> {{ getDataset.id }}
        </div>
        <div>
          <span class="font-weight-bold body-2">Dataset name:</span> {{ getDataset.name }}
        </div>
        <div>
          <span class="font-weight-bold body-2">Number of networks attached:</span> TODO
        </div>
        <div>
          <span class="font-weight-bold body-2">Description:</span> {{ getDataset.description }}
        </div>
        <div><span class="font-weight-bold body-2">Status:</span>
          <v-chip small v-if="getDataset.public" color="primary" text-color="white" style="font-size:11px;margin:0px;">Public</v-chip>
          <v-chip small v-else color="orange" text-color="white">Private</v-chip>
        </div>
        <div><span class="font-weight-bold body-2">Last update:</span>
          {{ formatUpdate }}
        </div>
      </div>
      <div class="title pt-4 teal--text">Citation</div>
      <v-divider class="pb-2"></v-divider>
      <v-flex pt-3 x12>
        <div v-if="getRef" class="text-md-left">{{ getCitation || 'None' }}<br>
        <v-btn v-if="getCitation" @click="exportBib()" small depressed outline color="teal" text-color="white" style="font-size:11px;margin:0px;text-transform: none !important;">Export as BibTex</v-btn>
        </div>
      </v-flex>
      <div class="title pt-4 teal--text">Sources</div>
      <v-divider class="pb-2"></v-divider>
      <v-flex x12>
        <div v-if="getRef" class="text-md-left">
          <div class="font-weight-bold body-2">Data URL</div><a :href="getRef.data_url">{{ getRef.data_url || "None" }}</a>
        </div>
        <div v-if="getRef" class="text-md-left">
          <div class="font-weight-bold body-2">Paper URL</div><a :href="getRef.paper_url">{{ getRef.paper_url || "None"}}</a>
        </div>
      </v-flex>
    </v-container>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import Cite from 'citation-js'
import { saveAs } from 'file-saver'
import moment from 'moment'
export default {
  method: {
    exportBib: function () {
      var blob = new Blob(this.getRef.bibtex, {type: 'text/plain;charset=utf-8'})
      saveAs(blob, 'bibtex.txt')
    }
  },
  computed: {
    ...mapGetters([
      'getRef',
      'getDataset'
    ]),
    getCitation: function bib2cite () {
      return new Cite(this.getRef.bibtex).format('bibliography', {
        type: 'json',
        template: 'apa',
        lang: 'en-US'
      })
    },
    formatUpdate: function format () {
      return moment(this.getDataset.updated_at).fromNow()
    }
  }
}
</script>
