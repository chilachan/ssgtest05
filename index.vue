<template>
  <section class="container">
    <h1>画面を変えていこう！</h1>
    <n-link to="test" class="button--green">test</n-link>
  </section>
</template>

<script>
import {mapState} from 'vuex';
export default {
  data: function() {
    return {
      content: '',
      find_flg: false
    }
  },
  computed: {
    ...mapState(['todos']),
    display_todos: function() {
      if(this.find_flg) {
        const arr = [];
        const data = this.todos;
        data.forEach(element => {
          if(element.content.toLowerCase() === this.content.toLowerCase()) {
            arr.push(element);
          }
        });
        return arr;
      } else {
        return this.todos;
      }
    }
  },
  methods: {
    insert: function() {
      this.$store.commit('insert', {content: this.content});
      this.content = '';
    },
    find: function() {
      this.find_flg = true;
    },
    set_flg: function() {
      if(this.find_flg) {
        this.find_flg = false;
        this.content = '';
      }
    },
    remove: function(todo) {
      this.$store.commit('remove', todo)
    },
    flag_reset: function(){
      this.find_flg = false;
    }
  }
}
</script>