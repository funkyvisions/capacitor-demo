<template>
  <div></div>
</template>

<script>

// import { Http } from '@capacitor-community/http'
import {onMounted} from "vue"
import { HTTP } from '@ionic-native/http'

export default {

  setup() {

    async function callHttp(url) {
      return new Promise((resolve) => {
        alert(`Calling ${url}`)
        // let response
        try {
          HTTP.setRequestTimeout(5)
          HTTP.sendRequest(url, { method: 'get', timeout: 5 },(a) => {
            alert("success " + JSON.stringify(a))
            resolve(a)
          }, (a) => {
            alert("failure " + JSON.stringify(a))
            resolve(a)
          })
        } catch(e) {
          alert("error " + e.message)
          // response = {
          //   message: e.message
          // }
        }
        // alert(JSON.stringify(response))
      })
    }

    onMounted(async() => {
      await callHttp('https://httpstat.us/200?sleep=1000')
      await callHttp('https://httpstat.us/200?sleep=15000')
      await callHttp('https://thisendpointdoesnotexist.com')
    })
  }
}

</script>
