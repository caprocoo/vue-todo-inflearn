<template>
  <div>
    <transition-group name="list" tag="ul">

      <li v-for=" (todoItem, index) in this.todoItems" v-bind:key="todoItem.item" class="shadow">
        <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}"
           v-on:click="toggleComplete({todoItem, index})"></i>

        <!-- todoItem.complete가 true면 class가 textCompleted로 적용 -->
        <span v-bind:class="{textCompleted: todoItem.completed}"> {{ todoItem.item }} </span>
        <span class="removeBtn" v-on:click="removeTodo({todoItem, index})">
        <i class="fas fa-trash-alt"></i>
      </span>
      </li>

    </transition-group>
  </div>
</template>

<script>
import {mapState, mapGetters, mapMutations} from 'vuex';

export default {

  computed:{
    // mapState로 store js에서 todoItems 가져오기
    ...mapState(['todoItems']),

    // mapGetters로 store js에서 todoItems 가져오기
    ...mapGetters(['storedTodoItems']),
  },
  methods: {


    // store mutation helper 사용
    ...mapMutations({
      removeTodo : 'removeOneItem',
      toggleComplete : 'toggleComplete'
    }),

    // store mutation 바로 호출 - remove
    // removeTodo (todoItem, index) {
    //
    //   // this.$emit('removeItem', todoItem, index)
    //   const payload = {
    //     todoItem : todoItem,
    //     index : index
    //   }
    //   this.$store.commit('removeOneItem', payload);
    //
    //
    // }

    // store mutation 바로 호출 - toggleComplete
    // toggleComplete(todoItem, index) {
    //
    //   // this.$emit('toggleItem', todoItem, index)
    //   const payload = {
    //     todoItem : todoItem,
    //     index : index
    //   }
    //
    //   this.$store.commit('toggleComplete', payload);
    // },

  },


}
</script>

<style scoped>

ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}

li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}

.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}

.checkBtnCompleted {
  color: #b3adad;
}

.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}

.removeBtn {
  margin-left: auto;
  color: #de4343;
}

/* 리스트 아이템 트랜지션 효과*/

.list-enter-active, .list-leave-active {
  transition: all 1s;
}

.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */
{
  opacity: 0;
  transform: translateY(30px);
}
</style>