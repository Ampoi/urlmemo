<template>
  <main class="bg-gray-200 h-screen w-screen pt-20 overflow-auto">
    <div class="mx-auto w-[350px]">
      <div class="h-[470px] bg-white rounded-xl text-center pt-10">
        <h1 class="text-4xl font-black">URLMEMO</h1>
        <p>URLからメモを保存・公開！</p>
        <textarea class="bg-gray-100 border-gray-200 border-2 resize-none rounded-lg mt-5 w-[330px] h-[200px] text-md p-3"
                  placeholder="ここにメモする文字を入力ー" v-model="fromText"></textarea>
        <button class="py-2 px-3 bg-sky-500 rounded-xl text-white font-bold mt-2"
                @click="makeURL"
        >URLを作成</button>
        <div class="bg-gray-100 border-gray-200 border-2 resize-none rounded-lg mt-5 w-[330px] h-[60px] text-md p-2 mx-auto
                    overflow-x-auto"
        >{{ toURL }}</div>
      </div>
      <div class="h-56 bg-white rounded-xl text-center p-3 mt-5">
        <p>リンクの文字↓</p>
        <div class="bg-gray-100 border-gray-200 border-2 resize-none rounded-lg mt-5 w-[330px] h-40 text-md p-2 mx-auto
                    overflow-x-auto"
        >{{  getMemo }}</div>
      </div>
    </div>
    <!--SNS-->
    <div class="text-center mt-5 text-gray-500">
      S.kuronosuke
      <div>
        <a href="https://github.com/shibata-kuronosuke" class="m-1">
          <i class="bi bi-github"></i>
        </a>
        <a href="https://twitter.com/Skuronosuke_o" class="m-1">
          <i class="bi bi-twitter"></i>
        </a>
      </div>
    </div>
  </main>
</template>

<style>
@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.8.0/font/bootstrap-icons.css");</style>

<script>
export default {
  data(){return{
    getMemo: "",
    fromText: "",
    toURL: ""
  }},
  mounted(){
    const getBase = (new URL(document.location)).searchParams.get("memo")
    const decoded = decodeURIComponent(atob(getBase));
    this.getMemo = decoded
  },
  methods: {
    makeURL(){
      const encoded = btoa(encodeURIComponent(this.fromText));
      this.toURL = `${ location.origin }/urlmemo/?memo=${encoded}`
      console.log(this.toURL)
      navigator.clipboard.writeText(this.toURL).then(e => {
        alert('コピーできました');
      });
    }
  }
}
</script>