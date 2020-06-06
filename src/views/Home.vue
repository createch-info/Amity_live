<template>
  <b-container fluid>
    <b-row>
        <b-col md="12" sm="12" class="ele1" style="padding:10px;color:red;font-weight:bold;background-color:#dadada"><i>
              Due to extenuating circumstances related to COVID-19 and the health and well- being of patients and staff being a primary focus, our regular seminar schedule has been postponed.
We will be transitioning our education events to webinar format  until further notice and will be offering additional webinars on high priority topics.  To stay up-to-date, please subscribe to our Listserv on our home page.
We apologize for the inconvenience!</i>
          </b-col>
    </b-row>
    <b-row>
      <b-col lg="8" sm="12" xs="12">
        <b-row style="align-items:center;padding:10px;">
        
          <b-col md="3" sm="3" class="ele1" style="padding:10px;">
          
          </b-col>
          <b-col md="3" sm="3" class="ele2" style="padding:10px;">
            <span style="background-color:#A9A9A9; padding:7px;">&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;&nbsp;
            <b style="font-size:15px;">Expired Sessions</b>
          </b-col>
          <b-col md="3" sm="3" class="ele3" style="padding:10px;">
            <span style="background-color:#007bff; padding:7px;">&nbsp;&nbsp;&nbsp;&nbsp;</span>&nbsp;&nbsp;
            <b style="font-size:15px;">Upcoming Sessions</b>
          </b-col>
          <b-col md="3" sm="3" class="ele4" style="padding:10px;">
            <!-- <button
              style="float: right; font-size:14px;"
              @click="changeYear(1)"
              class="btn btn-outline btn-primary responsive-changer-hidden"
            >
              Next
              <i class="fa fa-forward" aria-hidden="true"></i>
            </button> -->
          </b-col>
        </b-row>

        <b-row class="responsive-changer" style="align-items:center;padding:10px;">
          <b-col>
            <button
              @click="changeYear(-1)"
              class="btn btn-outline btn-primary"
              style="font-size:14px;"
            >
              <i class="fa fa-backward" aria-hidden="true"></i>
              Previous
            </button>
          </b-col>
          <b-col>
            <button
              style="float: right; font-size:14px;"
              @click="changeYear(1)"
              class="btn btn-outline btn-primary"
            >
              Next
              <i class="fa fa-forward" aria-hidden="true"></i>
            </button>
          </b-col>
        </b-row>

        <b-row>
          <b-col
            style="padding:10px;width:100%;"
            v-for="(index,month) in months"
            :key="index"
            lg="3"
            sm="3"
            xs="3"
          >
            <YearCalender :key="yearupdate" :currentDate="custdate(month,selectedYear)" />
          </b-col>
        </b-row>
        <!-- {{events}} -->
        <!-- <Calendar :loading="loading" :first-day="1" :all-events="events" :showWeekNumberFlag="true"></Calendar> -->
      </b-col>
      <b-col style="padding-top:20px;">
        <ListView></ListView>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import Calendar from "@/components/Calendra/Calendar";
import ListView from "@/components/ListView";
import EventBus from "./../eventBus";
import YearCalender from "./../components/Calendra/YearCalender";
import moment from "moment";

export default {
  components: {
    ListView: ListView,
    YearCalender: YearCalender
  },
  data() {
    return {
      months: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
      years: [],
      // changeYear:true,
      selectedYear: parseInt(moment().format("YYYY")),
      yearupdate: 1
    };
  },
  name: "home",
  created() {
    let i = 0;

    let year = parseInt(moment().format("YYYY"));

    while (i <= 10) {
      this.years.push({ value: year, text: year });
      year += 1;
      i++;
    }
  },
  methods: {
    changeYear(val) {
      this.selectedYear += val;
      this.onChange();
      // console.log('after',this.selectedYear);
      // this.custdate();
    },
    onChange() {
      this.yearupdate++;
    },
    custdate(month, selectedYear) {
      return moment(new Date(selectedYear, month, 1).toString());
    }
  }
};
</script>

<style scoped>
.col-sm-3 {
  width: auto;
}

.col-md-3 {
  width: auto;
}

.responsive-changer {
  /* display: none; */
}

@media (min-width: 768px) {
   .page_header[data-v-61dd7a3d] {
    font-size: 15px;
  }
}

@media (max-width: 767px) {
  .responsive-changer-hidden {
    display: none;
  }
  
  .responsive-changer {
    /* display: block; */
  }

  .ele1 {
    order: 1;
  }

  .ele4 {
    order: 1;
  }
}
/* 
.container-fluid, .container-sm, .container-md, .container-lg, .container-xl
{
      padding-right: 20px !important;
    padding-left: 20px !important;
} */
</style>

