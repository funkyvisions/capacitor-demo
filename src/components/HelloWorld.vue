<template>
  <div></div>
</template>

<script>

import { Http } from '@capacitor-community/http'
import {onMounted} from "vue"

export default {

  setup() {

    async function callHttp(url) {
      alert(`Calling ${url}`)
      let response
      try {
        response = await Http.get({
          url: url,
          connectTimeout: 10000,
          readTimeout: 10000
        })
      } catch(e) {
        response = {
          message: e.message
        }
      }
      alert(JSON.stringify(response))
    }

    onMounted(async() => {
      await callHttp('https://httpstat.us/200?sleep=1000')
      await callHttp('https://httpstat.us/200?sleep=15000')
      await callHttp('https://thisendpointdoesnotexist.com')
    })
  }
}

</script>
