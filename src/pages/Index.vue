<template>
  <q-page>
    <div class="q-ma-xl flex flex-center">
      <q-uploader
        url="http://localhost:3000"
        label="Send your image / PDF"
        field-name="pdf"
        @uploaded="uploaded"
      />
    </div>
    <div class="flex flex-center">
      <div v-if="pages.length">
        <q-input
        style="width: 320px;"
          width="400px"
          :label="`Extracted text page ${currentPage}:`"
          v-model="currentItem.text"
          filled
          type="textarea"
        />
        <div class="q-pa-lg flex flex-center" v-if="pages.length > 1">
          <q-pagination
            v-model="currentPage"
            :max="pages.length"
            @input="changePage"
          />
        </div>
      </div>
      <div v-else>
        No uploaded content
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      pages: [],
      currentPage: 1,
    }
  },
  computed: {
    currentItem () {
      return this.pages.find((page, index) => {
        return index + 1 === this.currentPage
      })
    }
  },
  methods: {
    uploaded (response) {
      this.pages = JSON.parse(response.xhr.response)
    },
    changePage (page) {
      this.currentPage = page
    }
  }
}
</script>
