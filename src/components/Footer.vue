<template>
 
  <footer class="bd-footer">

      <div class="blackfooter">
    <div class="container-fluid">
      <b-row style="margin:auto;" v-if='$route.name === "login"'>
          <b-col md="12" sm="12" class="ele1" style="margin-left:auto !important;	margin-right: auto !important;	color: #721c24 !important;	background-color: #f8d7da !important;	border-color: #f5c6cb !important;	border: 1px solid !important;	border-radius: .25rem !important;	position: center !important;	padding: 12px !important;"><i>
                Due to extenuating circumstances related to COVID-19 and the health and well- being of patients and staff being a primary focus, our regular seminar schedule has been postponed.
  We will be transitioning our education events to webinar format  until further notice and will be offering additional webinars on high priority topics.  To stay up-to-date, please subscribe to our Listserv on our home page.
  We apologize for the inconvenience!</i>
            </b-col>
      </b-row>
      <b-row class="wrap-builder-items" v-if='$route.name !== "login"'>
       
        <div class="col-md-4 icon1box">
          <div class="row">
          <div class="col-md-3 iconbx">
            <img src="../assets/icon1.png">
          </div>
          <div class="col-md-9 mdbox">
          <span class="smallfont">Call Us</span>
          <span class="bigfont">303-690-2749</span>
          </div>
          </div>
        </div>
        <div class="col-md-4 icon1box darkin">
          <div class="row">
          <div class="col-md-3 iconbx">
             <img src="../assets/icon2.png">
          </div>
          <div class="col-md-9 mdbox">
          <span class="smallfont">Email Us</span>
          <span class="bigfont">ig@amityhealthcaregroup.com</span>
          </div>
          </div>
        </div>

        <div class="col-md-4 icon1box">
          <div class="row">
          <div class="col-md-3 iconbx">
            <img src="../assets/icon3.png">
          </div>
          <div class="col-md-9 mdbox">
          <span class="smallfont">Fax </span>
          <span class="bigfont">720-398-6200</span>
          </div>
          </div>
        </div>
      
        
      </b-row>
    </div>
    </div>


    <div class="blackfooter">
    <div class="container-fluid">
      <b-row class="wrap-builder-items">
        <div class="col-md-2" style="padding:0px;">
          <ul class="fbranddiv">
            <li><img src="https://amityhealthcaregroup.com/wp-content/uploads/2019/03/amity-logo-1.png" class="footerbrand"></li>
            
          </ul>
          
        </div>
        <div class="col-md-10" style="padding:0px;">
          <ul class="footermenu">
            <li><a href="https://amityhealthcaregroup.com">Home</a></li>
            <li><a href="https://amityhealthcaregroup.com/about-us/">About Us </a></li>
            <li><a href="https://amityhealthcaregroup.com/consulting-services/">Consulting Services</a></li>
            <li><a href="https://amityhealthcaregroup.com/outsourcing-services/">Outsourcing Services</a></li>
            <li><a href="https://amityhealthcaregroup.com/education/#/">Education </a></li>
            <li><a href="https://amityhealthcaregroup.com/resources/">Resources </a></li>
            <li><a href="https://amityhealthcaregroup.com/contact/">Contact Us</a></li>

          </ul>
          
        </div>
      </b-row>
    </div>
    </div>
    <b-container>
      <div class="row copyrightcolumn">
      <div class="col-md-6">
        Copyright © 2019 Amity Healthcare Group. All rights reserved. 
      </div>
      <div class="col-md-6">
       <div class="menuright">
        <a href="https://amityhealthcaregroup.com/privacy-policy/" class="footernavi">Privacy Policy</a> 
        <a href="https://amityhealthcaregroup.com/terms-and-conditions/" class="footernavi">Terms and Conditions</a>
       </div>
      </div>
      </div>
      <b-row class="justify-content-md-center">
        <div class="bd-footer-copyright">Powered by <a href="#">CREATECH</a>
          leader in proven online marketing and web solutions for SMBs!!
        </div>
      </b-row>
    </b-container>
  </footer>
 
</template>

<style>

.bd-footer {
  margin-top: 2em;
  border-top: .2rem #f7f7f7 solid !important;
}

ul.footermenu li {
    display: inline;
    margin: 0px 12px;
}

ul.footermenu li a {
    color: #cccccc;
}
ul.footermenu li a:hover{
  color:#2e9ce6;
  text-decoration: none;
}



.blackfooter1 {
    BACKGROUND: #1f1f1f;
    padding: 0px 0px;
}


span.bigfont {
    font-size: 20px;
    display: block;
}
@media (min-width: 769px){
  .row.wrap-builder-items {
    width: 100%;
    margin: 0px auto;
}
.blackfooter {
    BACKGROUND: #1f1f1f;
    padding: 30px 0px;
}
.col-md-4.icon1box{
    background: #003f8c;
    color: #fff;
    padding: 15px;
    height:102px;
    margin-top: -30px!important;
}
.col-md-4.icon1box.darkin {
    background: #01234b;
}
.fbranddiv img{
  width: 220px;
}
.fbranddiv {
    padding: 3px;
}
ul.footermenu {
    float: right;
    line-height: 1.0!important;
    margin: 0px!important;
    padding-top:20px;
}
.bd-footer-copyright {
  padding-top: 2rem;
  padding-bottom: 2rem;
  color: #636363;
  font-size: 14px;
}
a.footernavi {
    color: #000;
    font-size: 18px;
    margin: 0px 10px;
}
}





a.footernavi {
  text-decoration: none!important;
}
.menuright{
  float: right;
}
.row.copyrightcolumn {
    padding: 15px;
    font-size: 14px;
}







@media(max-width:768px){
  .col-md-3.iconbx {
    width: 30%!important ;
    float: left;
  }
  span.bigfont{
    font-size: 16px!important;
  }
  .col-md-4.icon1box{
    background: #003f8c;
    color: #fff;
    padding: 15px;
    height:90px;
  }
  .row.wrap-builder-items {
    margin-top: 0px;
  }
  .col-md-4.icon1box.darkin {
    background: #01234b;
  }
  .fbranddiv img{
      width: 220px;
  }
  .fbranddiv{
  text-align: center;
  }
  .blackfooter {
    BACKGROUND: #1f1f1f;
    padding: 0px 0px;
}
  .blackfooter .col-md-9{
    width: 100%!important;
    text-align: center;
  }
  ul.footermenu {
    float: right;
    line-height: 3.0!important;
    margin: 0px!important;
}
.bd-footer-copyright {
    padding-top: 2rem;
    padding-bottom: 2rem;
    color: #636363;
    font-size: 14px;
    text-align: center;
    padding: 25px;
}
a.footernavi {
    color: #000;
    font-size: 16px;
    margin: 0px 15px;
}
.col-md-9.mdbox {
    float: left;
    width: 70%!important;
    text-align: left;
}
}
</style>
