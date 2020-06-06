<template>
  <div
    class="day-cell"
    :class="{ 'isBigFont':!issmall, 'isSmallFont':issmall,'minHieght':issmall,'hasEvent':day.hasEvent,'today' : day.isToday, 'current-month' : day.isCurrentMonth, 'weekend': day.isWeekEnd, 'selected-day':isDaySelected,'isPast':day.isPast,'tooltip-hover':day.hasEvent}"
    @click="showDayOptions" style="min-height:0px !important;"
  >
       <p style="position:relative" :class="{'style-text':day.hasEvent}" v-show="showable">{{ day.date.format('D') }}
        </p>
    <!-- <div class="row" >
      <div class="col-sm-12" :class="{'tooltip-hover':day.hasEvent}" >
        <p style="position:relative" :class="{'style-text':day.hasEvent}" v-show="showable">{{ day.date.format('D') }}
          
          <span v-if="day.hasEvent" class="tooltiptext">
            {{day.events.length > 0 ? day.events[0].title : ''}}
            
            <br/><br/>
            {{day.events[0].date_}}
            <br/>
            {{day.events[0].start_time+" - "+day.events[0].end_time}}

          </span>
        </p>
      </div>
    </div>
     -->

     <span v-if="day.hasEvent" class="tooltiptext">
            <div style="text-decoration:underline">{{day.events.length > 0 ? day.events[0].title : ''}}
            </div>
            <br/>
            {{day.events[0].date_}}
            <br/>
            {{day.events[0].start_time+" - "+day.events[0].end_time}}

          </span>
    <div v-if="!issmall" class="event-box">
     
      <event-card
        :event="event"
        :key="event.id"
        :day-date="day.date"
        :is-day-selected="isDaySelected"
        :is-past="day.isPast"
        v-for="event in day.events"
      ></event-card>
    </div>

    <!-- <slot name="is_curr"></slot> -->
  </div>
</template>

<script>

import moment from "moment";
import { DAY_SELECTED, CHANGE_MONTH } from "./actions";
export default {
  data() {
    return {
      isDaySelected: false
    };
  },
  components: {
    EventCard: require("./EventCard.vue").default
      ? require("./EventCard.vue").default
      : require("./EventCard.vue")
  },
  props: {
    customHeight:{
      type:String
    },
    dayselect:{
      type:Number,
				default:0,
    },
    showable:{
      type: Boolean,
    },
    issmall: {
      type: Boolean,
      default: false
    },
    day: {
      type: Object
    },
    firstDay: {
      type: String
    }
  },
  created() {
    let me = this;
    
    if(this.dayselect==this.day.date.format('D'))
    {
       me.isDaySelected = true;
        //alert(JSON.stringify(me.day));
       // this.isDaySelected=true;
    }

    this.$root.$on(DAY_SELECTED, function(payload) {
      if (payload.dayDate != me.day.date) {
        me.isDaySelected = false;
      }
    });

    this.$root.$on(CHANGE_MONTH, function() {
      me.isDaySelected = false;
    });
  },
  
  methods: {
    formatdate(date){
        return date;
    },
    showDayOptions() {
      console.log('showDayOptions')
      let me = this;
      let startOfToday = moment().startOf("day");
      // if (
      //   this.day.date.isAfter(startOfToday) ||
      //   this.day.date.isSame(startOfToday)
      // ) {
        this.isDaySelected = true;

        this.$root.$emit(DAY_SELECTED, { dayDate: me.day.date, event: me.day });
      // }
    },
    showAddEventForm() {}
  }
};
</script>
<style scoped>
.style-text{
  text-decoration: underline;
  color: black !important;
}

.tooltip-hover {
  position: relative;
  margin: 0%;
  top:0px;
  display: inline-block;

}

.tooltip-hover .tooltiptext{
    visibility: hidden;
    width: 250px;
    font-size: 16px;
    background-color: #007bff;
    color: #fff;
    text-align: center;
    border-radius: 6px;
    padding: 5px 5px;
    position: absolute;
    z-index: 1;
    bottom: 103%;
    left: 50%;
    margin-left: -122px;
    opacity: 0;
    /* -webkit-transition: opacity .3s; */
    transition: opacity .3s;
}
/* .tooltip-hover .tooltiptext
{
    visibility: hidden;
    width: 250px;
    font-size: 16px;
    background-color: #007bff;
    color: #fff;
    text-align: center;
    border-radius: 6px;
    padding: 5px 5px;
    position: absolute;
    z-index: 1;
    bottom: 125%;
    left: 50%;
    margin-left: -60px;
    opacity: 0;
    -webkit-transition: opacity .3s;
    transition: opacity .3s;
  
    } */
.tooltip-hover .tooltiptext::after {
  /* content: ""; */
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  /* border-color: #555 transparent transparent transparent; */
}

.tooltip-hover:hover .tooltiptext {
  visibility: visible;
  opacity: 1;
  
}



@media(min-width:769px)  {
.minHieght {
  min-height: 50px !important;
}
.current-month p {
  color: #000;
  padding: 15px 0px 0px 0px;
  font-size: 26px;
  text-align: center;
}
.hasEvent {
  background-color: #0078d7 !important;
  cursor:pointer !important
}
.hasEvent p {
  color: "white" !important;
}
.hasEvent.isPast {
  background-color:#A9A9A9 !important;
  cursor: pointer !important
}
.hasEvent.day-number {
  color: white !important;
}
.hasEvent.isPast.day-number {
  color: rgba(0, 0, 0, 0.5) !important;
}

/* .day-cell:hover{
  background-color: #000000;
} */

.day-cell {
  flex: 1;
  min-height: 110px;
  /* padding: 4px; */
  /* border-right: 1px solid #e0e0e0;
  border-bottom: 1px solid #e0e0e0; */
  /* background: rgba(147, 147, 147, 0.1); */
  /* border-left: solid 5px transparent; */
}

.day-number {
  font-weight: 900;
  text-align: right;
  color: #c1c1c1;
  font-size: 1em;
  padding: 5px;
}

.current-month {
  background: #f4f4f4;
}

.selected-day.hasEven p {
  font-size: 2.4em;
  font-weight: bolder;
}

.selected-day.hasEvent {
  border: solid 5px #000000;
  color: #fff !important;
  
  padding: 0px !important;
}
.weekend p {
  color: #000;
}

.today p {
  color: #259b24;
}
.day-cell.hasEvent.current-month p {
  color: #fff;
}
.hasEvent.isPast p {
  color:black !important;
}
.isBigFont p {
  color: #000;
  padding: 15px 0px 0px 0px;
  font-size: 26px !important;
  text-align: center;
}
/* .week-row{
  cursor:'unset !important'
}
.week-row.hasEvent{
  cursor:'pointer !important'
} */
.isSmallFont p {
  color: #000;
  font-size: 11px !important;
  text-align: center;
  padding: 5px 0px;
}


}





















@media (max-width:768px) {
  

.minHieght {
  min-height: 50px !important;
}
.current-month p {
  color: #000;
  padding: 15px 0px 0px 0px;
  font-size: 26px;
  text-align: center;
}
.hasEvent {
  background-color: #0078d7 !important;
  cursor:pointer !important
}
.hasEvent p {
  color: "white" !important;
}
.hasEvent.isPast {
  background-color: #9a9a9a !important;
  cursor: unset !important
}
.hasEvent.day-number {
  color: white !important;
}
.hasEvent.isPast.day-number {
  color: rgba(0, 0, 0, 0.5) !important;
}
.day-cell {
  flex: 1;
  min-height: 52px;
  padding: inherit;
  border-right: 1px solid #e0e0e0;
  border-bottom: 1px solid #e0e0e0;
  background: rgba(147, 147, 147, 0.1);
  border-left: solid 5px transparent;
  border-left: solid 2px #e7e5e5;
}

.day-number {
  font-weight: 900;
  text-align: right;
  color: #c1c1c1;
  font-size: 1em;
  padding: 5px;
}

.current-month {
  background: #f4f4f4;;
}

.selected-day.hasEven p {
  font-size: 2.4em;
  font-weight: bolder;
}

.selected-day.hasEvent {
  border: solid 5px #000000;
  color: #fff !important;
  height: 60px;
  padding: 0px !important;
}
.weekend p {
  color: #000;
}

.today p {
  color: #259b24;
}
.day-cell.hasEvent.current-month p {
  color: #fff;
}
.hasEvent.isPast p {
  color:black !important;
}
.isBigFont p {
    color: #000;
    padding: 5px 0px 0px 0px;
    font-size: 16px !important;
    text-align: center;
}
.isSmallFont p {
  color: #000;
  font-size: 16px !important;
  text-align: center;
  padding: 5px 0px;
}
.event-title{
  display: none!important;
}
/* .week-row{
  cursor:'unset !important'
}
.week-row.hasEvent{
  cursor:'pointer !important'
} */

.col-sm-4 {
    width: 33.33%!important;
    float: left;
}
.title{
  font-size: 16px!important;
}
button.btn.btn-outline.btn-primary {
    padding: 2px 2px!important;
    font-size: 12px!important;
    width: 80px!important;
}
.label01 {
    font-weight: 800;
    color: #000;
    text-align: left;
    width: 40%!important;
    padding: 15px 5px;
    font-size: 14px;
    float: left;
}
.label02 {
    text-align: left;
    width: 60%;
    float: left;
    font-size: 14px;
    font-weight: 800;
    padding: 15px 5px;
}
}
</style>