<template>
 <div v-if="DASH_VISIBLE" class="container">
     <div class="tasks shadow">
         <cards-comp page="GeneralTasks" title="GENERAL TASKS" color="#0B3591" v-bind:stats="GEN_TOTAL" />
         <cards-comp title="CRITICAL TASKS" color="#C40D0D" stats="120" />
         <cards-comp title="ASSIGN TASKS" color="#1BB444" v-bind:stats="ASSIGN_TOTAL" />
         <cards-comp title="RECENT ARCHIVED" color="#E5D655" stats="330" />
     </div>
     <div class="body">
         <div class="stats shadow">
             <chart />
         </div>
         <div class="spartans shadow">
             <div class="title">Online</div>
             <div class="contents">
                 <online-cards v-for="spartan in listOfOnline" :spartan="spartan" :key="spartan.user_id" />
             </div>
         </div>
     </div>
 </div>
</template>

<script>
import OnlineCards from '@/components/Spartans/OnlineCards.vue'
import CardsComp from './CardsComp.vue'
import { mapGetters, mapActions } from 'vuex'
import Chart from '@/components/Dashboard/Chart/Chart'

export default {
  name: 'DashComp',
  components: { CardsComp, OnlineCards, Chart },
  computed: { ...mapGetters(['USER_ID', 'listOfOnline', 'totalUsers', 'ORGAID', 'GEN_TOTAL', 'ASSIGN_TOTAL', 'DASH_VISIBLE']) },
  data () {
    return {
      datacollection: null
    }
  },
  mounted () {
    this.fillData()
    this.getOpenTasks(this.ORGAID)
    this.getAssignTasks(this.USER_ID)
    if (this.DASH_VISIBLE) return

    setTimeout(() => {
      this.changeVisibility(true)
    }, 2000)
  },
  methods: {
    ...mapActions(['getOpenTasks', 'getAssignTasks', 'changeVisibility']),
    fillData () {
      this.datacollection = {
        labels: [this.getRandomInt(), this.getRandomInt()],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '#f87979',
            data: [this.getRandomInt(), this.getRandomInt()]
          }, {
            label: 'Data One',
            backgroundColor: '#f87979',
            data: [this.getRandomInt(), this.getRandomInt()]
          }
        ]
      }
    },
    getRandomInt () {
      return Math.floor(Math.random() * (50 - 5 + 1)) + 5
    }
  }
}
</script>

<style scoped>
.container{
    margin: 0 auto;
    margin-top: 20px;
    height: 88%;
    overflow: auto;
}
.contents{
    margin: 0 auto;
    width: 84%;
    height: 380px;
    margin-top: 20px;
    overflow:hidden;
}

  .contents:hover{
     overflow: auto;
  }
  .contents::-webkit-scrollbar{
    width: 10px;
    border-radius: 20px;
  }

  /* Track */
  .contents::-webkit-scrollbar-track {

    width: 1px;
    border-radius: 4px;
    box-shadow: inset 0 0 10px 10px;
    border: solid 3px transparent;
  }

  /* Handle */
  .contents::-webkit-scrollbar-thumb {

    width:2px;
    border-radius: 10px;
    background: rgb(139, 10, 10);
  }

.shadow{
    box-shadow: 2px 5px 10px #888888;
}
.tasks{
    display: grid;
    grid-template-columns: auto auto auto auto;
    width: 90%;
    height: 240px;
    padding: 14px;
    border-radius: 20px;
    background: white;
    margin: 0 auto;
    gap: 14px;
}
.body{
    display: grid;
    grid-template-columns: auto auto;
    padding: 18px;
    height: 60%;
    margin: 0 auto;
}
.stats{
    margin: 0 auto;
    height: 500px;
    margin-left: 40px;
    width: 70%;
    border-radius: 20px;
    background: white;
    text-align: center;
}
.spartans{
    border-radius: 20px;
    background: white;
    height: 90%;
    margin: 0 auto;
    width: 64%;
    display: grid;
    grid-template-rows: auto auto;
}
.title{
    position: relative;
    margin-top: 20px;
    margin-left: 20px;
    font-size: x-large;
    height: 10px;
    color: #646464;
    font-weight: bolder;
}

</style>
