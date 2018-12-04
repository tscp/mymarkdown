<template>
  <div id="terms">
    <div class="terms-container">
      <h1>利用規約</h1>
      <p>本サイトはテスト目的で作成されました。</p>
      <p>
        ソースコードは <a href="https://twitter.com/nabettu">@nabettu</a> さんの<a href="https://www.amazon.co.jp/dp/4844398350">書籍</a>を元にして作成されています。
        実際のコードは<a href="https://github.com/nabettu/mymarkdown">こちら</a>に上がっていますが、私が本を読みながらだましだまし手で打ったものになります。
      </p>
      <p>Markdown 部分は <a href="https://www.npmjs.com/package/marked">marked</a> という便利な npm ライブラリを使用しています。</p>
      <p>Vue.js と Firebase の連携や Github へ push したデータを Netlify へ自動デプロイといった来たるべき新しいワークフローを試して体験したものになります。</p>
      <p>上述の理由により、本サービスはあくまでもテスト目的のため、作成したデータの保証、バグやその他いかなる不具合に関しても一切責任は追わないものといたします。</p>
    </div>
    <router-link :to="{ name:'top' }">TOP に戻る</router-link>
  </div>
</template>

<script>
export default {
  name: 'terms'
};
</script>

<style lang="scss" scoped>
#terms > div {
  max-width: 640px;
  text-align: left;
  margin: 60px auto;
  line-height: 1.8;
  h1 {
    font-size: 2rem;
    font-weight: bold;
    margin-bottom: 1rem;
  }
  p {
    margin-bottom: .5rem;
  }
}
</style>

