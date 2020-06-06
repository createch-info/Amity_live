<template>
    <div>
        <b-list-group v-if="load">
            <b-list-group-item active><b>Upcoming Events</b></b-list-group-item>
              <div class="events-list scrollbar" id="style-3">
                <!-- getevents(loadMore) -->
                <b-list-group-item :key="index"  v-for="(data,index) in this.reviews" style="background-color:rgba(147, 147, 147, 0.1)" :href="'#/booking/'+data.id" class="flex-column align-items-start">
                  <div class="d-flex w-100 justify-content-between">
                    <h5 class="mb-1">{{data.date}}</h5>
                  </div>

                  <p class="mb-1">
                      <!-- <small v-html="reviews[index].format"></small> -->
                      <span style="text-decoration:underline" v-html="data.title"></span>
                  </p>
                </b-list-group-item>
              </div>
            </b-list-group>
          <!-- <b-list-group-item active>
            <button style="border-radius:2px;outline:none;padding:3px;" v-if="loadMore" @click="getevents(loadMore)">Load More</button>
          </b-list-group-item>   -->
    </div>
</template>

<script>
export default {
    data:()=>{
        return {
            mesg:'hello',
            load:true,
            loadMore:false,
            reviews: [],
            commentsToShow: 1
        }       
    },
    computed:{
      
    },
    created()
    {
          this.$http.get("seminar/eventlist").then(success => {
          this.commentsToShow=success.length;
          
          this.loadMore=success.pagination.loadmore
          
          this.reviews=success.data;
          this.load=true;
        });
      
    },
    methods:{
        // if ($(window).scrollTop() >= ($(document).height() - $(window).height())*0.7){


        getevents(url)
        {
              this.$http.get(url).then(success => {
              this.commentsToShow=success.length;
              
              this.loadMore=success.pagination.loadmore
               
              success.data.forEach(element => {
                  this.reviews.push(element);
                
              });
          
              this.load=true;
            });
        }
    }  

}

</script>

<style scoped>
  .events-list{
    height:976px;
    /* height:100%; */
    overflow-x:hidden;
    overflow-y: scroll;
  }  
  


#style-3::-webkit-scrollbar-track
{
	background-color: #F5F5F5;
}

#style-3::-webkit-scrollbar
{
	width: 6px;
	background-color: #F5F5F5;
}

#style-3::-webkit-scrollbar-thumb
{
	background-color: #007bff;
}

</style>