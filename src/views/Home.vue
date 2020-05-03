<template>
  <div class="home">
    <div class="main">
        <div class="leftNotes">
            <button @click="newNot" class="newNote">
                <i class="far fa-edit"></i> Create Note
            </button>
            <div class="forNotes">
                <template v-if="notes.length > 0">
                    <Notes v-for="(note, index) in notes" :note="note" @noteClick="select" :index="index" />
                </template>
                <article v-else style="text-align: center; padding-top: 20px">
                    No rating
                </article>
            </div>
        </div>
      <Writter :note="current_note" />
      <!--      <arti:note="noteClick"cle v-for="(note, index) in notes">-->
<!--        <article>{{ note.id }}</article>-->
<!--        <article>{{ note.content }}</article>-->
<!--      </article>-->
    </div>
  </div>
</template>

<style scoped>

    .forNotes{
        overflow-y: scroll;
        height: calc(100% - 69px)
    }
    .newNote{
        width: 100%;
        padding: 20px 0px;
        cursor: pointer;
        background-color: #0080ff;
        border: none;
        outline: none;
        font-size: 110%;
        border-bottom: 1px solid #eaeaea;
        color: white;
    }

    .forNotes{
        overflow-y: scroll;
    }

    .leftNotes{
        border-right: 1px solid lightgrey;
        width: 270px;
        text-align: left;
    }
  .home{
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .main{
    width: 95vw;
    height: 95vh;
    box-shadow: 0px 0px 5px lightgrey;
    display: flex;
      border-radius: 10px;
      overflow: hidden;
  }

</style>
<script>
// @ is an alias to /src
import { mapGetters , mapActions} from 'vuex'
import Notes from "../components/Notes";
import Writter from "../components/Writter";
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    Notes, Writter
  },

  data(){
    return{
      noteClick:{
        created_at: '',
        content: '',
      }
    }
  },

  created() {
    this.$store.dispatch('load_notes');
  },

  computed: {
    ...mapGetters(['notes']),
     ...mapGetters(['current_note'])
  },

  methods: {
      ...mapActions(['add_current_note']),
    select(param){
      console.log(param)
      this.noteClick = param
        this.add_current_note(param)
    },

      newNot(){
        this.noteClick = {
            content: ''
        }
          this.add_current_note(this.noteClick)
      }
  }

}
</script>
