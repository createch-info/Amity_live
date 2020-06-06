<template>
    <Calendar customheight="28px" :issmall="true" :currentDate="currentDate" :loading="loading" :first-day="1" :all-events="events" :showWeekNumberFlag="true"></Calendar>
</template>

<script>
import Calendar from "./Calendar";

export default {
    props:{
        currentDate:{
			  // type:String,
			  default:moment().toString()
			},
    },
    components:{
        Calendar:Calendar,
    },
    created() 
    {
        let _this = this;
        this.loadData(this.currentDate);
        
        this.$root.$on("CHANGE_MONTH", function(date) 
        {
            _this.loadData(date);
        });
        // this.$root.$on("EVENT_SELECTED", function(event) {
        //   _this.eventSelected(event)
        // });
        this.$root.$on("DAY_SELECTED", function(date) {
        if(date.event.events.length > 0){
            _this.eventSelected(date.event.events[0])
        }
        
        });
    },
    methods: {
     loadData(start_date) {
      this.loading = true;
      this.$http
        .get("seminar", {
          params: {
            start_date: start_date.toString()
          }
        })
        .then(responce => {
          this.events = responce;
          this.loading = false;
        })
        .catch(error => {
          this.loading = false;
        });
    },
    eventSelected(ev) {
    if(this.$route.name != 'home') return
      if (ev.isFull) {
        this.$router.push({ name: "bookingFully" });
      } else {
        this.$router.push({ name: "booking", params: { id: ev.id } });
      }
    },
  },
    data:()=>{
        return {
            events: [],
            loading:true
        }
    }
}
</script>

<style scoped>
    
</style>