<template>
  <v-container grid-list-xs>
    <h1 class="primary--text mt-4">Question</h1>    
    <Post v-model="$store.state.question" tipe="Question" :key="$store.state.question._id"/>
    <h1 class="success--text mt-4">Answer</h1>
    <Post v-model="$store.state.question.answers[index]" v-for="(answer,index) in $store.state.question.answers" tipe="Answer" :key="answer._id"/>
    <v-card class="mt-5">
    <!-- v-show="$store.state.answered" -->
      <v-container>
        <h1>Post Answer to this question</h1>
        <PostForm @submitted="answerQuestion"/>
      </v-container>
    </v-card>
  </v-container>
</template>

<script>
// import { mapState } from 'vuex'
import Post from '@/components/Post'
import PostForm from '@/components/PostForm'

export default {
  components: {
    Post,
    PostForm
  },
  data(){
    return {
    }
  },
  computed: {
  },
  // watch: {
  //   '$store.state.answered'(){
  //   this.$store.dispatch('getQuestion',this.$route.params.id)
  // },
  // },
  created(){
    this.$store.dispatch('getQuestion',this.$route.params.id)
  },
  methods: {
    answerQuestion(title,description){
      this.$store.dispatch('answerQuestion',{
        questionid: this.$store.state.question._id,
        title,
        description
      })
    },
  }
}
</script>
