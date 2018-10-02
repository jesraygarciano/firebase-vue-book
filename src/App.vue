    <template>
      <div id="app">
          <Notebook @change-page="changePage" @new-page="newPage" :pages="pages" :activePage="index" />
          <Page @save-page="savePage" @delete-page="deletePage" :page="pages[index]" />
      </div>
    </template>

    <script>
    import Notebook from './components/Notebook'
    import Page from './components/Page'
    import Firebase from 'firebase'

   var database = Firebase.initializeApp({
      apiKey: 'AIzaSyDG02SKCHwfaWdNR4rylICg1KBE9U70lpM',
      authDomain: 'gartbook-852fd.firebaseapp.com',
      databaseURL: 'https://gartbook-852fd.firebaseio.com',
      projectId: 'gartbook-852fd',
      storageBucket: 'gartbook-852fd.appspot.com',
      messagingSenderId: '427192969962'
  }).database().ref();
   
    export default {
      name: 'app',
      components: {
        Notebook,
        Page
      },
      data: () => ({
        pages: [],
        index: 0
      }),
      methods: {
        newPage () {
          this.pages.push({
            title: '',
            content: ''
          })
          this.index = this.pages.length - 1
        },
        changePage (index) {
          this.index = index
        },
        savePage () {
           // nothing as of yet
        },
        deletePage () {
          this.pages.splice(this.index, 1)
          this.index = Math.max(this.index - 1, 0)
        }
      }
    }
    </script>

    <style>
    html, body, #app {
        height: 100%;
    }

    body {
        margin: 0;
    }

    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        display: flex;
        flex-direction: row;
    }
    </style>
