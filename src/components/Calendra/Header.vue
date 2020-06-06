<template>
  <div class="row">
    <div v-if="monthchanger" class="col-sm-4">
      <button @click.stop="goPrev" class="btn btn-outline btn-primary" style="font-size:14px;width:100%">
        <i class="fa fa-backward" aria-hidden="true"></i>
        Previous
      </button>
    </div>

    <div class="header-center" :class="{'col-md-12':monthchanger,'col-md-12':!monthchanger}">
      <div class="title">{{title}}</div>

      <!-- <div class="btn-group"> -->

      <!-- <button @click.stop="goToday" class="btn btn-outline btn-default today-button">&dArr; Today</button> -->

      <!-- </div> -->
    </div>
    
    <div v-if="monthchanger" class="col-sm-4">
      <button style="float: right; font-size:14px;width:100%" @click.stop="goNext" class="btn btn-outline btn-primary" >
        Next
        <i class="fa fa-forward" aria-hidden="true"></i>
      </button>
    </div>

  </div>
</template>
<script>
import moment from "moment";
import { CHANGE_MONTH } from "./actions";
import EventBus from './../../eventBus'
export default {
  data() {
    return {
      localeSelect: "en"
    };
  },
  props: {
    monthchanger:{
      type:Boolean,
      default:false
    },
    currentMonth: {},
    locale: {
      type: String
    }
  },
  computed: {
    title() {
      if (!this.currentMonth) return;
      return this.currentMonth.locale(this.locale).format("MMMM YYYY");
    }
  },
  methods: {
    goPrev() {
      let payload = moment(this.currentMonth)
        .subtract(1, "months")
        .startOf("month");
      this.$root.$emit(CHANGE_MONTH, payload);
    },
    goNext() {
      let payload = moment(this.currentMonth)
        .add(1, "months")
        .startOf("month");
       
     this.$root.$emit(CHANGE_MONTH, payload);
    },
    goToday() {
      this.$root.$emit(CHANGE_MONTH, moment());
    },
    setLocale() {
      
    }
  }
};
</script>
<style>
.full-calendar-header {
  display: flex;
  align-items: center;
}
.header-center {
  flex: 3;
  text-align: center;
}
.title {
  text-align: center;
  padding:10px;
  font-size: 1.2em;
  font-weight: bolder;
}
.language-select {
  display: inline-block;
  width: 50%;
}
</style>