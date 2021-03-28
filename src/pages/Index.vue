<template>
  <q-page class="flex flex-center">
    <q-uploader
      url="http://192.168.0.23:3000"
      label="Send your image / PDF"
      :headers="headers"
      field-name="pdf"
    />
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  methods: {
    headers () {
      return [{name: 'Content-Type', value: 'multipart/form-data'}]
    }
  }
}
</script>
