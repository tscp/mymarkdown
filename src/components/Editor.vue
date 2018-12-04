<template>
  <div class="editor">
    <div class="editorHead">
      <h1>Markdown Editor</h1>
      <div class="editorUser">
        <span>{{ user.displayName }}</span>
        <button @click="logout">ログアウト</button>
      </div>
    </div>
    <div class="editorWrapper">
      <div class="memoListWrapper">
        <div class="memoList" v-for="(memo, index) in memos" :key="index" @click="selectMemo(index)" :data-selected="index == selectedIndex">
          <p class="memoTitle">{{ displayTitle(memo.markdown) }}</p>
        </div>
        <button class="addMemoBtn --primary" @click="addMemo">メモの追加</button>
        <button class="deleteMemoBtn --attention" v-if="memos.length > 1" @click="deleteMemo">選択中のメモの削除</button>
        <button class="saveMemosBtn --secondary" @click="saveMemos">メモの保存</button>
      </div>
      <textarea class="markdown" v-model="memos[selectedIndex].markdown" placeholder="何かここに書く"></textarea>
      <div class="preview markdown-body" v-html="preview()"></div>
    </div>
  </div>
</template>

<script>
  import marked from "marked";
  import Header from "./Header";
  export default {
    name: "editor",
    components: Header,
    props: ["user"],
    data() {
      return {
        memos: [
          {
            markdown: ""
          }
        ],
        selectedIndex: 0
      };
    },
    created: function() {
      firebase
        .database()
        .ref("memos/" + this.user.uid)
        .once("value")
        .then(result => {
          if(result.val()) {
            this.memos = result.val();
          }
        })
    },
    mounted: function() {
      document.onkeydown = e => {
        if (e.key == "s" && (e.metaKey || e.ctrlKey)) {
          this.saveMemos();
          return false;
        }
      }
    },
    beforeDestroy: function() {
      document.onkeydown = null;
    },
    methods: {
      logout: function() {
        firebase.auth().signOut();
      },
      addMemo: function() {
        this.memos.push({
          markdown: "無題のメモ"
        });
      },
      deleteMemo: function() {
        this.memos.splice(this.selectedIndex, 1);
        if(this.selectedIndex > 0) {
          this.selectedIndex--;
        }
      },
      selectMemo: function(index) {
        this.selectedIndex = index;
      },
      preview: function() {
        return marked(this.memos[this.selectedIndex].markdown);
      },
      displayTitle: function(text) {
        return text.split(/\n/)[0];
      },
      saveMemos: function() {
        firebase
          .database()
          .ref("memos/" + this.user.uid)
          .set(this.memos);
      }
    }
  };
</script>

<style lang="scss" scoped>
  .editorHead {
    display: flex;
    align-items: center;
    justify-content: space-between;
    text-align: left;
    padding: 24px 30px 0;
    h1 {
      font-size: 2rem;
      font-weight: bold;
    }
  }
  .editorUser {
    display: flex;
    align-items: center;
    button {
      margin-left: 20px;
    }
  }
  
  .editorWrapper {
    display: flex;
    justify-content: space-between;
    margin: 2%;
  }
  .memoListWrapper {
    width: 20%;
    border-top: 1px solid #efefef;
  }
  .memoList {
    padding: 10px;
    box-sizing: border-box;
    text-align: left;
    border-bottom: 1px solid #efefef;
    &:nth-child(even) {
      background-color: #eaeaea;
    }
    &[data-selected="true"] {
      background-color: #35495e;
      color: #fff;
    }
  }
  .memoTitle {
    height: 1.5em;
    margin: 0;
    white-space: nowrap;
    overflow: hidden;
  }
  .addMemoBtn {
    margin-top: 20px;
  }
  .markdown {
    width: 40%;
    height: 72vh;
    background: #fafafa;
    border: solid 1px transparent;
    &:focus {
      border: 1px solid #ababab;
      outline: none;
    }
  }
  .preview {
    width: 40%;
    text-align: left;
    // border: solid 1px #ababab;
  }
  .deleteMemoBtn {
    margin: 10px;
  }

  button {
    border: #fff;
    border-radius: 40px;
    box-shadow: 0 2px 8px rgba(0,0,0,.2);
    background: #f2f2f2;
    color: #666;
    cursor: pointer;
    padding: 10px 40px;
    margin: 10px;
    &:hover {
      background: #efefef;
    }
    &.--primary {
      background: #41b883;
      color: #fff;
      &:hover {
        background: #3ca777;
      }
    }
    &.--secondary {
      background: #35495e;
      color: #fff;
      &:hover {
        background: #28384a;
      }
    }
    &.--attention {
      background: #f17c67;
      color: #fff;
      &:hover {
        background: #d05f4b;
      }
    }
  }
</style>