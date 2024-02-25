<template>
  <div style="background-color:rgb(245, 245, 245); width:100%; height:100%;">
    <br>
    
    <div class="hero-wrap hero-wrap-2 js-fullheight" style="height:1400px;" data-stellar-background-ratio="0.5">
      <div style="width: 1200px; position: absolute; margin-left: 100px;">
        <div >
          <br>
          <br>
          <br>
          <br>
          <br>
          <h1 class="text-center" style=" opacity: 0; /* Set initial opacity to 0 for fade-in effect */
    animation: fade-up 0.8s ease-out forwards;font-size: 20px; font-weight:900; margin-left:50px; margin-top:2px;">BOOK YOUR <span style="font-size: 30px; font-weight:100;">|</span>&nbsp;&nbsp; <span style="font-size:70px; font-weight:400; font-family: 'WindSong', cursive;">Events...</span></h1>
          <br>
          <div>


            <button
            v-for="(item, index) in servinfo"
            :key="index"
            @click="openDialogs(item)"
            type="button"
            class="room-item text-center"
            style="
              opacity: 0;
              animation: fade-up 0.8s ease-out forwards;
              animation-delay: 0.2s;
              background-color: rgb(255, 255, 255);
              width: 260px;
              height: 330px;
              margin-left: 30px;
              margin-top: -10px;
              border-radius:9px;
            "
          >
            <div>
              <img
              :src="item.image"
              alt="Service Image"
              v-if="item.image"
              style="
                position: absolute;
                box-shadow: 3px 2px 2px rgba(0, 0, 0, 0.2);
                border-radius: 6px;
                width: 260px;
                height: 260px; /* Set the actual height of the image */
                overflow: hidden;
                clip: rect(0, 260px, 180px, 0); /* Clip the image to show only the upper 220 pixels */
                margin-left: -130px;
                top:-1px;
              "
            />
            
            <span
            style="
            width:200px;
              position: absolute;
              margin-left: -104px;
              margin-top: 60px;
              font-size: 17.3px;
              font-weight:400;
              text-align: left;
              color:#1b1b1b; font-family: 'Roboto', sans-serif;
            "
          >₱&nbsp;{{ item.low_pricing }}<span style="color:rgb(168, 168, 168); font-size:13px;"> / price</span></span>
              <span
                style="
                width:200px;
                  position: absolute;
                  margin-left: -104px;
                  margin-top: 90px;
                  font-size: 17.3px;
                  font-weight:500;
                  text-align: left;
                  color:#1b1b1b;font-family: 'Poppins', sans-serif;
                "
              >{{ item.service }}</span>
              <span style="display:none;">{{ item.id }}</span>
              <span
                style="
                  position: absolute;
                  margin-left: -104px;
                  font-size: 13px;
                  font-weight:900px;
                  margin-top: 135px;
                  color: rgb(22, 103, 255);
                  font-family: 'Roboto', sans-serif;font-family: 'Poppins', sans-serif;
                "
              >Avail Service <span style="font-size:20px;margin-left:6px; font-weight:300; position:absolute; top:-4px;"> ></span></span>
            </div><br>
            
          </button>

          <!-- @click="openDialog(item)" this is bookingform the form dialog -->


<!--                 
<div class="calendar-container" style="   opacity: 0; /* Set initial opacity to 0 for fade-in effect */
animation: fade-up .8s ease-out forwards;
animation-delay: 0.4s;position: absolute; margin-left:700px; top: 160px;">

  <v-row>
    <v-col cols="12">
      <h2 style=" font-family: 'Bebas Neue', cursive; ">Event Schedules</h2>
      <ul>
        <li v-for="event in approvedRequests" :key="event.id">
          {{ event.event_title }} - {{ formatDate(event.start_date) }} to {{ formatDate(event.end_date) }}
        </li>
      </ul>
    </v-col>
  </v-row>


  <div >
    <label for="month">Select Month:</label>
        <select id="month" v-model="selectedMonth" @change="updateCalendar">
          <option v-for="(month, index) in months" :key="index" :value="index">{{ month }}</option>
        </select>
    <label for="year">Select Year:</label>
        <select id="year" v-model="selectedYear" @change="updateCalendar">
          <option v-for="year in years" :key="year" :value="year">{{ year }}</option>
        </select>
  </div>
  <div >
    <table style="width: 440px; height: 400px;">
      <thead>
        <tr>
          <th colspan="7">{{ currentMonth }} {{ selectedYear }}</th>
        </tr>
        <tr>
          <th v-for="day in days" :key="day">{{ day }}</th>
        </tr>
      </thead>
        <tbody>
          <tr v-for="week in calendar" :key="week">
            <td v-for="day in week" :key="day.number"
              :class="{ highlighted: day.highlighted, today: isToday(day), eventDay: hasEvent(day) }">
              {{ day.number }}
            </td>
          </tr>
        </tbody>
    </table>
  </div>
  </div> -->
  
            
          </div>
          <br>
        </div>

    
    </div>
    </div>
    
  
   
    <div class="ftco-footer ftco-bg-dark ftco-section">
      <div class="container">
        <div class="row mb-5">
          <div class="col-md">
            <div class="ftco-footer-widget mb-4">
              <h2 class="ftco-heading-2">QMJ IMAGES ENTERPRISES</h2>
              <p>Your best source of Photography and Videography
Sound and stage lights production.</p>
              <ul class="ftco-footer-social list-unstyled float-md-left float-lft mt-5">
                <li class="ftco-animate"><a href="#"><span class="icon-twitter"></span></a></li>
                <li class="ftco-animate"><a href="#"><span class="icon-facebook"></span></a></li>
                <li class="ftco-animate"><a href="#"><span class="icon-instagram"></span></a></li>
              </ul>
            </div>
          </div>
          <div class="col-md">
            <div class="ftco-footer-widget mb-4 ml-md-5">
              <h2 class="ftco-heading-2">Useful Links</h2>
              <ul class="list-unstyled">
                <li><a href="#" class="py-2 d-block">Speakers</a></li>
                <li><a href="#" class="py-2 d-block">Shcedule</a></li>
                <li><a href="#" class="py-2 d-block">Events</a></li>
                <li><a href="/userblog" class="py-2 d-block">Blog</a></li>
              </ul>
            </div>
          </div>
          <div class="col-md">
             <div class="ftco-footer-widget mb-4">
              <h2 class="ftco-heading-2">Privacy</h2>
              <ul class="list-unstyled">
                <li><a href="/bookevents" class="py-2 d-block">Book Event</a></li>
                <li><a href="/about" class="py-2 d-block">About Us</a></li>
                <li><a href="/contacts" class="py-2 d-block">Contact Us</a></li>
                <li><a href="/userServices" class="py-2 d-block">Services</a></li>
                <li><a href="/userproducts" class="py-2 d-block">Products</a></li>
              </ul>
            </div>
          </div>
          <div class="col-md">
            <div class="ftco-footer-widget mb-4">
              <h2 class="ftco-heading-2">Want more Answers to your Questions?</h2>
              <div class="block-23 mb-3">
                <ul>
                  <li><span class="icon icon-map-marker"></span><span class="text">km. 13 BIGA, Calapan, Philippines</span></li>
                  <li><a href="Tel:0947 406 2928"><span class="icon icon-phone"></span><span class="text">0947 406 2928</span></a></li>
                  <li><a href="mailto:qmjimages2018@gmail.com"><span class="icon icon-envelope"></span><span class="text">qmjimages2018@gmail.com</span></a></li>
                  
                </ul>
              </div>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col-md-12 text-center">
  
          </div>
        </div>
      </div>
    </div>
  </div>


 <v-dialog v-model="dialogs" max-width="500px">
  <form @submit.prevent="saveBooking" class="container">
    <v-card>
      <br>
      <v-card-title class="headline" style="margin-left: 130px; font-size: 14px; font-weight:900;  ">REQUEST<span style="font-size: 22px;  font-weight:100;">&nbsp;&nbsp;|&nbsp;</span><span style="font-weight:400; font-family: 'WindSong', cursive; font-size:33px;">Form</span></v-card-title>
      <v-card-text>

        <div class="form-group">
          <label for="event_title">Selected Service:</label>
          <input type="text" class="search-input" style="width:100%; height:45px; border: none;" placeholder="" v-model="selectedService.service" readonly>
        </div>

        <div class="form-group">
          <label for="total_cost">Total Cost:</label>
          <input type="text" class="search-input" style="width:100%; height:45px; border: none;" placeholder="" v-model="computedTotal" readonly>
        </div>

        <div class="form-group">
          <label for="total_cost">Added Items:</label>
          <input type="text" class="search-input" style="width:100%; height:45px; border: none;" placeholder="" v-model="computedTotal" readonly>
        </div>

        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="start_date">Start Date:</label>
            <input type="date" class="neumorphic-button" style="width:100%; background-color:white; border-radius:3px;" v-model="start_date" required>
          </div>

          <div class="form-group col-md-6">
            <label for="end_date">End Date:</label>
            <input type="date" class="neumorphic-button" style="width:100%; background-color:white; border-radius:3px;" v-model="end_date" required>
          </div>
        </div>

        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="location">Location:</label>
            <input type="text" class="search-input" style="width:206%;height:60%" placeholder="Location" v-model="location" required>
          </div>
        </div>

        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="event_description">Description:</label>
            <textarea class="search-input" v-model="event_description" style="width:206%; height:60%;" placeholder="Other Description" required></textarea>
          </div>
        </div>

        <br><br>
        <h3 style="margin-left: 95px; font-size: 14px; font-weight:900;" >CONTACT<span style="font-size: 22px;  font-weight:100;">&nbsp;&nbsp;|&nbsp;</span><span style="font-weight:400; font-family: 'WindSong', cursive; font-size:33px;">Details</span></h3>
        <br>
        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="name">Name:</label>
            <input type="text" class="search-input" style="width:206%;height:70%;" placeholder="Name" v-model="name" required>
          </div>
        </div>

        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="email">Email:</label>
            <input type="email" class="search-input" style="width:206%;height:70%;" placeholder="Email Address" v-model="email" required>
          </div>
        </div>

        <div class="form-group">
          <label for="phone">Phone:</label>
          <input type="tel" class="search-input" style="width:100%;height:50px;;" placeholder="09*********" v-model="phone" required>
        </div>

      </v-card-text>
      <v-card-actions>

        <div style="margin-bottom: 10px;">
          <button type="submit" class="neumorphic-button" style="margin-left: 10px; width: 320%; background-color: rgb(49, 48, 48); color: white;">Book Event</button>
        </div>

      </v-card-actions>

    </v-card>
  </form>
</v-dialog> 



                <!-- booking dialog-->
<!-- <v-dialog v-model="dialogs" max-width="500px">
  <form @submit.prevent="saveBooking" class="container">
    <v-card>
      <br>
      <v-card-title class="headline" style="margin-left: 130px; font-size: 14px; font-weight:900;  ">REQUEST<span style="font-size: 22px;  font-weight:100;">&nbsp;&nbsp;|&nbsp;</span><span style="font-weight:400; font-family: 'WindSong', cursive; font-size:33px;">Form</span></v-card-title>
      <v-card-text>

        <div class="form-group">
          <label for="event_title">Event Title:</label>
          <input type="text" class="search-input" style="width:100%; height:45px;" placeholder="Event Title" v-model="event_title" required>
        </div>

        <div class="form-group">
          <label for="service">Services</label>
          <div class="position-relative">
            <select class="neumorphic-button" style="width:100%;" v-model="service" required>
              <option value="" disabled selected>Select a service</option>
              <option value="Sounds Service">Sounds Service</option>
              <option value="Lights Service">Lights Service</option>
              <option value="Photo Shoot Service">Photo Shoot Service</option>
              <option value="Video Shoot Service">Video Shoot Service</option>
              <option value="Photo & Video Shoots Service">Photo & Video Shoots Service</option>
              <option value="Photo & Video Shoots Service With SDE">Photo & Video Shoots Service With SDE</option>
              <option value="Sounds & Lights Service">Sounds & Lights Service</option>
              <option value="Sounds & Lights with Photo Shoot Service">Sounds & Lights with Photo Shoot Service</option>
              <option value="Sounds and Lights with Photo & Video Shoots Service">Sounds and Lights with Photo & Video Shoots Service</option>
              <option value="Sounds and Lights with Photo Video Shoots and SDE Service">Sounds and Lights with Photo Video Shoots and SDE Service</option>
            </select>
            <i class="fas fa-caret-down position-absolute end-0 bottom-0 p-3" style="pointer-events: none; top:-5px;"></i>
          </div>
        </div>

        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="start_date">Start Date:</label>
            <input type="date" class="neumorphic-button" style="width:100%; background-color:white; border-radius:3px;" v-model="start_date" required>
          </div>

          <div class="form-group col-md-6">
            <label for="end_date">End Date:</label>
            <input type="date" class="neumorphic-button" style="width:100%; background-color:white; border-radius:3px;" v-model="end_date" required>
          </div>
        </div>

        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="location">Location:</label>
            <input type="text" class="search-input" style="width:206%;height:60%" placeholder="Location" v-model="location" required>
          </div>
        </div>

        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="event_description">Description:</label>
            <textarea class="search-input" v-model="event_description" style="width:206%; height:60%;" placeholder="Other Description" required></textarea>
          </div>
        </div>

        <br><br>
        <h3 style="margin-left: 95px; font-size: 14px; font-weight:900;" >CONTACT<span style="font-size: 22px;  font-weight:100;">&nbsp;&nbsp;|&nbsp;</span><span style="font-weight:400; font-family: 'WindSong', cursive; font-size:33px;">Details</span></h3>
        <br>
        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="name">Name:</label>
            <input type="text" class="search-input" style="width:206%;height:70%;" placeholder="Name" v-model="name" required>
          </div>
        </div>

        <div class="form-row">
          <div class="form-group col-md-6">
            <label for="email">Email:</label>
            <input type="email" class="search-input" style="width:206%;height:70%;" placeholder="Email Address" v-model="email" required>
          </div>
        </div>

        <div class="form-group">
          <label for="phone">Phone:</label>
          <input type="tel" class="search-input" style="width:100%;height:50px;;" placeholder="09*********" v-model="phone" required>
        </div>

      </v-card-text>
      <v-card-actions>

        <div style="margin-bottom: 10px;">
          <button type="submit" class="neumorphic-button" style="margin-left: 10px; width: 320%; background-color: rgb(49, 48, 48); color: white;">Book Event</button>
        </div>

      </v-card-actions>

    </v-card>
  </form>
</v-dialog> -->




<!--service info dialog-->
<v-dialog v-model="dialogss" max-width="900px">
  <form @submit.prevent="saveBooking" class="container">
    <v-card style="height:550px;">
      <br>
      <v-card-title class="headline text-center" style="font-size: 14px; font-weight:900;  ">SERVICE<span style="font-size: 22px;  font-weight:100;">&nbsp;&nbsp;|&nbsp;</span><span style="font-weight:400; font-family: 'WindSong', cursive; font-size:33px;">Information</span></v-card-title>
      <v-card-text>
       
        <v-card-text class="headline text-center" style="font-size: 14px; font-weight:900; margin-top:-25px;">
          {{ selectedService.service }} 
        </v-card-text>

        <div style=" margin-left:20px; width:150px;" class="neumorphic-navbars" >
        <v-card-text class="headline text-left" style="">
          <img :src="selectedService.image" style="height:120px; height:120px;" alt="Service Image">
        </v-card-text>
        </div>

        <v-card-text class="headline text-left" style="position:absolute; top:22%; left:36%; width:350px; font-size: 14px; font-weight:400;">
         &nbsp;&nbsp;{{ selectedService.information }} 
        </v-card-text>  

        <br>
  <!-- &nbsp;&nbsp;Minimum Price:{{ formatPrice(selectedService.low_pricing) }} old pricing method convert 1000 into 1k -->
  <span>
    <v-card-text class="headline text-left" style="position:absolute; top:49%; left:5%; width:350px; font-size: 14px; font-weight:600;">
      &nbsp;&nbsp;Minimum Price: {{ displayMinimumPrice }}
    </v-card-text>
  </span>
        
        <span><v-card-text class="headline text-left" style="position:absolute; top:55%; left:5%; width:350px; font-size: 14px; font-weight:600;">
          &nbsp;&nbsp;Request for additional item quantity:
         </v-card-text>  </span>
         
        <button
        type="button"
        @click="openDialogss(selectedService.first_req)"
        
        style="
          position:absolute;
          opacity: 0;
          animation: fade-up 0.8s ease-out forwards;
          animation-delay: 0.2s;
          background-color: rgb(255, 255, 255);
          width: 164px;
          height: 50px;
          margin-left: 20px;
          margin-top: 75px;
          border-radius:3px;
        "
      >{{ selectedService.first_req }} - {{ selectedService.first_price }} 
      </button>

        <input type="number" class="search-input"  inputmode="numeric"  style="
        position:absolute;
        opacity: 0;
        animation: fade-up 0.8s ease-out forwards;
        animation-delay: 0.2s;
        background-color: rgb(255, 255, 255);
        width: 154px;
        height: 50px;
        margin-left: 20px;
        margin-top: 125px;
        border-radius:3px;
      " placeholder="0"  v-model="inputValue" @input="updateMinimumPrice" >

      <button
        type="button"
        @click="openDialogss(selectedService.second_req)"
        
        style="
          position:absolute;
          opacity: 0;
          animation: fade-up 0.8s ease-out forwards;
          animation-delay: 0.2s;
          background-color: rgb(255, 255, 255);
          width: 164px;
          height: 50px;
          margin-left: 190px;
          margin-top: 75px;
          border-radius:3px;
        "
      >{{ selectedService.second_req }} - {{ selectedService.second_price }} 
      </button>

      <input type="number" class="search-input"  inputmode="numeric"  style="
      position:absolute;
      opacity: 0;
      animation: fade-up 0.8s ease-out forwards;
      animation-delay: 0.2s;
      background-color: rgb(255, 255, 255);
      width: 154px;
      height: 50px;
      margin-left: 196px;
      margin-top: 125px;
      border-radius:3px;
    " placeholder="0" v-model="secondInputValue" @input="updateMinimumPrice"  >

      <button
      type="button"
      @click="openDialogss(selectedService.third_req)"
    
      style="
        position:absolute;
        opacity: 0;
        animation: fade-up 0.8s ease-out forwards;
        animation-delay: 0.2s;
        background-color: rgb(255, 255, 255);
        width: 164px;
        height: 50px;
        margin-left: 360px;
        margin-top: 75px;
        border-radius:3px;
      "
    >{{ selectedService.third_req }} - {{ selectedService.third_price }} 
    </button>

    <input type="number" class="search-input"  inputmode="numeric"  style="
    position:absolute;
    opacity: 0;
    animation: fade-up 0.8s ease-out forwards;
    animation-delay: 0.2s;
    background-color: rgb(255, 255, 255);
    width: 154px;
    height: 50px;
    margin-left: 370px;
    margin-top: 125px;
    border-radius:3px;
  " placeholder="0" v-model="thirdInputValue" @input="updateMinimumPrice"  >

      <button
        type="button"
        @click="openDialogss(selectedService.fourth_req)"
       
        style="
          position:absolute;
          opacity: 0;
          animation: fade-up 0.8s ease-out forwards;
          animation-delay: 0.2s;
          background-color: rgb(255, 255, 255);
          width: 164px;
          height: 50px;
          margin-left: 20px;
          margin-top: 182px;
          border-radius:3px;
        "
      >{{ selectedService.fourth_req }} - {{ selectedService.fourth_price }} 
      </button>

      <input type="number" class="search-input"  inputmode="numeric"  style="
      position:absolute;
      opacity: 0;
      animation: fade-up 0.8s ease-out forwards;
      animation-delay: 0.2s;
      background-color: rgb(255, 255, 255);
      width: 154px;
      height: 50px;
      margin-left: 20px;
      margin-top: 230px;
      border-radius:3px;
    " placeholder="0" v-model="fourthInputValue" @input="updateMinimumPrice" >


      <button
      type="button"
      @click="openDialogss(selectedService.fifth_req)"
     
      style="
        position:absolute;
        opacity: 0;
        animation: fade-up 0.8s ease-out forwards;
        animation-delay: 0.2s;
        background-color: rgb(255, 255, 255);
        width: 164px;
        height: 50px;
        margin-left: 190px;
        margin-top: 182px;
        border-radius:3px;
      "
    >{{ selectedService.fifth_req }} - {{ selectedService.fifth_price }} 
    </button>

    <input type="number" class="search-input"  inputmode="numeric"  style="
    position:absolute;
    opacity: 0;
    animation: fade-up 0.8s ease-out forwards;
    animation-delay: 0.2s;
    background-color: rgb(255, 255, 255);
    width: 154px;
    height: 50px;
    margin-left: 196px;
    margin-top: 230px;
    border-radius:3px;
  " placeholder="0"  v-model="fifthInputValue" @input="updateMinimumPrice" >

    <button
    type="button"
    @click="openDialogss(selectedService.sixth_req)"
   
    style="
      position:absolute;
      opacity: 0;
      animation: fade-up 0.8s ease-out forwards;
      animation-delay: 0.2s;
      background-color: rgb(255, 255, 255);
      width: 164px;
      height: 50px;
      margin-left: 360px;
      margin-top: 182px;
      border-radius:3px;
    "
  >{{ selectedService.sixth_req }} - {{ selectedService.sixth_price }} 
  </button>


  <input type="number" class="search-input"  inputmode="numeric"  style="
    position:absolute;
    opacity: 0;
    animation: fade-up 0.8s ease-out forwards;
    animation-delay: 0.2s;
    background-color: rgb(255, 255, 255);
    width: 154px;
    height: 50px;
    margin-left: 370px;
    margin-top: 230px;
    border-radius:3px;
  " placeholder="0" v-model="sixthInputValue" @input="updateMinimumPrice" >


      <button
      type="button"
      @click="openDialog(item)"
      class="neumorphic-button"
      style="
        position:absolute;
        background-color: rgb(51, 50, 50);
        width: 155px;
        height: 40px;
        margin-left:370px;
        margin-top: 318px;
        border-radius:3px;
        color:white;
        
      "
    >File Request
    </button>

    <li class="menu-item" >
    <a
      type="button"
      @click="openDialogsss()"
      class="neumorphic-button"
      style="
        position:absolute;
        opacity: 0;
        animation: fade-up 0.8s ease-out forwards;
        animation-delay: 0.2s;
        background-color: rgb(255, 255, 255);
        width: 169px;
        height: 40px;
        margin-left: 354px;
        margin-top: 15px;
        border-radius:3px;
      "
    > Show Added Items
    </a>
    </li>

   

        <v-card-text class="headline text-left" style=" font-size: 14px; font-weight:400; margin-top:50%;">
          &nbsp;   &nbsp;&nbsp;
        </v-card-text>     

      </v-card-text>
      <v-card-actions>
      
      </v-card-actions>
    </v-card>
  </form>
</v-dialog>




<v-dialog v-model="dialogssss" max-width="400px">
  <form @submit.prevent="saveBooking" class="container">
    <v-card style="height:360px;">
      <br>
      <v-card-title class="headline text-center" style="height:40px;font-size: 14px; font-weight:900;   ">  Added Items</v-card-title>
      <v-card-title class="headline text-center" style="height:40px;font-size: 14px; font-weight:400; margin-top:-15px; ">  Added Quantity of the items</v-card-title>
      <v-card-text>

        <div>{{ selectedService.first_req }}: {{ inputValue || '0' }}     &nbsp;&nbsp;&nbsp;(added item price: {{ first_totalPrice }}) <span style="display:none;">{{ selectedService.first_price }}</span></div>
        <div>{{ selectedService.second_req }} : {{ secondInputValue || '0' }}    &nbsp;&nbsp;&nbsp; (added item price: {{ second_totalPrice }}) <span style="display:none;">{{ selectedService.second_price }}</span></div>
        <div>{{ selectedService.third_req }} : {{ thirdInputValue || '0' }}     &nbsp;&nbsp;&nbsp;(added item price: {{ third_totalPrice }}) <span style="display:none;">{{ selectedService.third_price }}</span></div>
        <div>{{ selectedService.fourth_req }} : {{ fourthInputValue || '0' }}     &nbsp;&nbsp;&nbsp;(added item price: {{ fourth_totalPrice }}) <span style="display:none;">{{ selectedService.fourth_price }}</span></div>
        <div>{{ selectedService.fifth_req }} : {{ fifthInputValue || '0' }}     &nbsp;&nbsp;&nbsp;(added item price: {{ fifth_totalPrice }}) <span style="display:none;">{{ selectedService.fifth_price }}</span></div>
        <div>{{ selectedService.sixth_req }} : {{ sixthInputValue || '0' }}    &nbsp;&nbsp;&nbsp; (added item price: {{ sixth_totalPrice }}) <span style="display:none;">{{ selectedService.sixth_price }}</span></div>
        <br>
        <div>Added items total price: {{ totalSum }}</div>
        <div>Minimum price: {{selectedService.low_pricing}}</div>
        <div>Total cost: {{ (parseFloat(totalSum) + parseFloat(selectedService.low_pricing)).toFixed(2).replace(/\.0+$/, '') }}</div>

        
      </v-card-text>
      <v-card-actions>
      
      </v-card-actions>
    </v-card>
  </form>
</v-dialog>


  </template>
  
  
  <script>
  import axios from 'axios'

  export default {
  data() {
    return {
      inputValue: "",
      secondInputValue: "",
      thirdInputValue: "",
    fourthInputValue: "",
    fifthInputValue: "",
    sixthInputValue: "",
      selectedServiceInDialog: null,
      selectedService: {},
      selectedService: null,
      retrievedService: "",
      servinfo: [],
      dialogs: false,
      dialogss: false,
      dialogsss: false,
      dialogssss: false,
      selectedMonth: new Date().getMonth(),
      selectedYear: new Date().getFullYear(),
      days: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
      months: [
        'January', 'February', 'March', 'April', 'May', 'June',
        'July', 'August', 'September', 'October', 'November', 'December'
      ],
      approvedRequests: [ /* Your approved events data */ ],
      calendar: [],

        event_title:"", 
        start_date:"", 
        end_date:"", 
        location:"", 
        event_description:"", 
        name:"", 
        email:"", 
        phone:"", 
        service:"",
      info: [],
    }
  },
  computed: {
    computedTotal() {
      const sum = parseFloat(this.totalSum) + parseFloat(this.selectedService.low_pricing);
      return sum.toFixed(2).replace(/\.0+$/, '');
    },
  
    first_totalPrice: function() {
      const inputNumber = parseFloat(this.inputValue) || 0;
      const result = inputNumber * this.selectedService.first_price;
      const formattedResult = result % 1 === 0 ? result.toFixed(0) : result.toFixed(2);
      return formattedResult;
    },
    second_totalPrice: function() {
      const inputNumber = parseFloat(this.secondInputValue) || 0;
      const result = inputNumber * this.selectedService.second_price;
      const formattedResult = result % 1 === 0 ? result.toFixed(0) : result.toFixed(2);
      return formattedResult;
    },
    third_totalPrice: function() {
      const inputNumber = parseFloat(this.thirdInputValue) || 0;
      const result = inputNumber * this.selectedService.third_price;
      const formattedResult = result % 1 === 0 ? result.toFixed(0) : result.toFixed(2);
      return formattedResult;
    },
    fourth_totalPrice: function() {
      const inputNumber = parseFloat(this.fourthInputValue) || 0;
      const result = inputNumber * this.selectedService.fourth_price;
      const formattedResult = result % 1 === 0 ? result.toFixed(0) : result.toFixed(2);
      return formattedResult;
    },
    fifth_totalPrice: function() {
      const inputNumber = parseFloat(this.fifthInputValue) || 0;
      const result = inputNumber * this.selectedService.fifth_price;
      const formattedResult = result % 1 === 0 ? result.toFixed(0) : result.toFixed(2);
      return formattedResult;
    },
    sixth_totalPrice: function() {
      const inputNumber = parseFloat(this.sixthInputValue) || 0;
      const result = inputNumber * this.selectedService.sixth_price;
      const formattedResult = result % 1 === 0 ? result.toFixed(0) : result.toFixed(2);
      return formattedResult;
    },
    totalSum: function() {
  const sum =
    parseFloat(this.first_totalPrice) +
    parseFloat(this.second_totalPrice) +
    parseFloat(this.third_totalPrice) +
    parseFloat(this.fourth_totalPrice) +
    parseFloat(this.fifth_totalPrice) +
    parseFloat(this.sixth_totalPrice);

  const formattedSum = sum.toFixed(2).toString();

  // Remove the trailing .00
  const totalWithoutDecimal = formattedSum.endsWith('.00') ? formattedSum.slice(0, -3) : formattedSum;

  return totalWithoutDecimal;
},
    displayMinimumPrice() {
    const firstInputMultiplier = this.inputValue === "" ? 0 : parseInt(this.inputValue);
    const secondInputMultiplier = this.secondInputValue === "" ? 0 : parseInt(this.secondInputValue);
    const thirdInputMultiplier = this.thirdInputValue === "" ? 0 : parseInt(this.thirdInputValue);
    const fourthInputMultiplier = this.fourthInputValue === "" ? 0 : parseInt(this.fourthInputValue);
    const fifthInputMultiplier = this.fifthInputValue === "" ? 0 : parseInt(this.fifthInputValue);
    const sixthInputMultiplier = this.sixthInputValue === "" ? 0 : parseInt(this.sixthInputValue);

    const calculatedPrice =
      firstInputMultiplier * this.selectedService.first_price +
      secondInputMultiplier * this.selectedService.second_price +
      thirdInputMultiplier * this.selectedService.third_price +
      fourthInputMultiplier * this.selectedService.fourth_price +
      fifthInputMultiplier * this.selectedService.fifth_price +
      sixthInputMultiplier * this.selectedService.sixth_price +
      parseInt(this.selectedService.low_pricing);

    return calculatedPrice.toString();
  },
    displaySecondPrice() {
    if (this.secondInputValue === "") {
      return 0; // Default value if no input
    } else {
      return parseInt(this.secondInputValue) * this.selectedService.second_price;
    }
  },
  displayThirdPrice() {
    if (this.thirdInputValue === "") {
      return 0; // Default value if no input
    } else {
      return parseInt(this.thirdInputValue) * this.selectedService.third_price;
    }
  },
  displayFourthPrice() {
    if (this.fourthInputValue === "") {
      return 0; // Default value if no input
    } else {
      return parseInt(this.fourthInputValue) * this.selectedService.fourth_price;
    }
  },
  displayFifthPrice() {
    if (this.fifthInputValue === "") {
      return 0; // Default value if no input
    } else {
      return parseInt(this.fifthInputValue) * this.selectedService.fifth_price;
    }
  },
  displaySixthPrice() {
    if (this.sixthInputValue === "") {
      return 0; // Default value if no input
    } else {
      return parseInt(this.sixthInputValue) * this.selectedService.sixth_price;
    }
  },
    currentMonth() {
      return this.months[this.selectedMonth];
    },
     approvedRequests() {
      return this.info.filter(item => item.status === 'approved');
    },
    years() {
  const currentYear = new Date().getFullYear();
  const yearsBefore = 10;
  const yearsAfter = 10;
  const years = [];

  for (let i = currentYear - yearsBefore; i <= currentYear + yearsAfter; i++) {
    years.push(i);
  }

  return years;
}
  },
  created() {
    this.getEventInfo();
  },
  mounted() {
    this.updateCalendar();
    this.getInfo(); 
  },
  
  watch: {
  secondInputValue: function () {
    this.updateMinimumPrice();
  },
  thirdInputValue: function () {
    this.updateMinimumPrice();
  },
  fourthInputValue: function () {
    this.updateMinimumPrice();
  },
  fifthInputValue: function () {
    this.updateMinimumPrice();
  },
  sixthInputValue: function () {
    this.updateMinimumPrice();
  },
},
  methods: {

    updateMinimumPrice() {
      // You can add any additional logic here if needed
      // This method is called whenever the user input changes
    },
    formatPrice(price) {
      if (price >= 1e6) {
        return (price / 1e6).toFixed(price % 1e6 !== 0 ? 1 : 0) + 'M';
      } else if (price >= 1e3) {
        return (price / 1e3).toFixed(price % 1e3 !== 0 ? 1 : 0) + 'K'; // Add 'K' only for values in the thousands
      } else {
        return price.toString(); // Keep the original value for smaller values
      }
    },

    async getInfo() {
      try {
        const response = await axios.get('getservice');
        this.servinfo = response.data;
      } catch (error) {
        console.error(error);
      }
    }, 

    openDialog() {
    this.dialogs = true;
  },
    closeDialog() {
      this.dialogs = false;
    },
    openDialogs(item) {
      this.selectedService = item; // Set the selected service information
      this.dialogss = true; // Open the dialog
    },

    closeDialogs() {
      this.dialogss = false;
    },
    openDialogss(req) {
      this.dialogsss = true;
      this.retrievedService = req;
    },

    closeDialogss() {
      this.dialogsss = false;
    },
    
    openDialogsss() {
      this.dialogssss = true;
    },

    closeDialogsss() {
      this.dialogssss = false;
    },
    updateCalendar() {
    const firstDay = new Date(this.selectedYear, this.selectedMonth, 1).getDay();
    const lastDate = new Date(this.selectedYear, this.selectedMonth + 1, 0).getDate();
    const calendar = [];
    let date = 1;

    for (let i = 0; i < 6; i++) {
      const week = [];

      for (let j = 0; j < 7; j++) {
        if (i === 0 && j < firstDay) {
          week.push({ number: '', event: false, approvedEvent: null, highlighted: false });
        } else if (date > lastDate) {
          break;
        } else {
          const currentDate = new Date(this.selectedYear, this.selectedMonth, date);
          const isEventDay = this.hasEventOnDate(date);
          const approvedEvent = isEventDay ? this.getApprovedEvent(currentDate) : null;

          let highlighted = false; // Initialize highlighted flag to false

          if (approvedEvent) {
            // Check if the current date falls within the start_date and end_date of an approved event
            highlighted = currentDate >= new Date(approvedEvent.start_date) &&
                          currentDate <= new Date(approvedEvent.end_date);
          }

          week.push({
            number: date,
            event: isEventDay,
            approvedEvent: approvedEvent,
            highlighted: highlighted, // Update highlighted flag
          });

          date++;
        }
      }

      calendar.push(week);
      if (date > lastDate) break;
    }

    this.calendar = calendar;
  },

  getApprovedEvent(date) {
  return this.approvedRequests.find(event => {
    const eventStartDate = new Date(event.start_date);
    const eventEndDate = new Date(event.end_date);

    return date >= eventStartDate && date <= eventEndDate;
  });
},
hasEventOnDate(date) {
    const currentDate = new Date(this.selectedYear, this.selectedMonth, date);

    return this.approvedRequests.some(event => {
      const eventStartDate = new Date(event.start_date);
      const eventEndDate = new Date(event.end_date);

      // Check if the current date falls within the event's start and end dates
      return currentDate >= eventStartDate && currentDate <= eventEndDate;
    });
  },
    formatDate(date) {
      // Add your formatting logic for the event dates
      // Example: Format the date to your preferred format
      return new Date(date).toLocaleDateString();
    },
    isToday(day) {
      const today = new Date();
      return today.getFullYear() === this.selectedYear &&
        today.getMonth() === this.selectedMonth &&
        today.getDate() === day.number;
    },
    hasEvent(day) {
      return day.event;
    },
    async approveEvent() {
    try {
      const response = await axios.post('/updateEventStatus', {
        id: this.selectedEvent.id,
        status: 'approved'
      });

      if (response.status === 200) {
        // Update the status in the selectedEvent object
        this.showModal = false; // Close the modal after approval
        this.selectedEvent.status = 'approved';
        this.getEventInfo();

        // Find the index of the updated event in the info array and update it
        const index = this.info.findIndex(event => event.id === this.selectedEvent.id);
        if (index !== -1) {
          this.$set(this.info, index, { ...this.selectedEvent });
        }

        this.showModal = false; // Close the modal
      } else {
        console.error('Error updating event status');
      }
    } catch (error) {
      console.error('Error updating event status:', error);
    }
  },
  async getEventInfo() {
      try {
        const response = await axios.get('getevent');
        this.info = response.data;
      } catch (error) {
        console.error(error);
      }
    },
    async saveBooking() {
  try {
    // Display a confirmation dialog
    const userConfirmed = window.confirm('Are you sure you want to save?');

    // Check if the user clicked OK
    if (userConfirmed) {
      const ins = await axios.post("saveBooking", {
        event_title: this.event_title,
        start_date: this.start_date,
        end_date: this.end_date,
        location: this.location,
        event_description: this.event_description,
        name: this.name,
        email: this.email,
        phone: this.phone,
        service: this.service,
      });

      // Clear form fields after successful save
      this.event_title ="";
      this.start_date ="";
      this.end_date ="";
      this.location ="";
      this.event_description ="";
      this.name ="";
      this.email ="";
      this.phone ="";
      this.service ="";

      // Emit event and perform other actions
      this.$emit('data-saved');
     
      this.dialogs = false;
    }
    // If the user clicked Cancel, do nothing
  } catch (error) {
    console.error(error);
  }
},

  }
};
  </script>
  
  <style scoped> 
  .room-item {
    background-color: #ffffff;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
    transition: transform 0.3s ease-in-out;
  }
  
  .room-item:hover {
    background-color: rgba(250, 164, 4, 0.993);
    transform: scale(1.05);
  }
  .calendar-container {
    position: absolute;
    margin-left: 700px;
    top: 160px;
    background-color: #e0e5ec; /* Background color */
    box-shadow: 8px 8px 15px #babecc, -8px -8px 15px #ffffff; /* Neumorphic shadow */
    border-radius: 4px; /* Rounded corners */
    padding: 20px;
  }

  .calendar-container {
    position: absolute;
    margin-left: 700px;
    top: 160px;
    background-color: rgba(255, 255, 255, 0.5); /* Transparent background */
    backdrop-filter: blur(10px); /* Adding blur effect */
    border-radius: 4px; /* Rounded corners */
    padding: 20px;
  }

  /* Select boxes */
  select {
    padding: 8px;
    border-radius: 4px;
    border: 1px solid rgba(255, 255, 255, 0.5); /* Transparent border */
    margin-right: 10px;
    background-color: rgba(255, 255, 255, 0.3); /* Transparent background for select */
  }

  /* Table styles */
  table {
    width: 450px;
    height: 450px;
    border-collapse: collapse;
    margin-top: 15px;
    backdrop-filter: blur(5px); /* Adding blur effect */
    border-radius: 4px; /* Rounded corners */
    border: 1px solid rgba(255, 255, 255, 0.3); /* Transparent border */
  }

  th {
    padding: 10px;
    text-align: center;
    background-color: rgba(255, 255, 255, 0.3); /* Transparent background for table header */
  }

  td {
    padding: 10px;
    text-align: center;
    border: 1px solid rgba(255, 255, 255, 0.3); /* Transparent border */
    background-color: rgba(255, 255, 255, 0.2); /* Transparent background for table cell */
  }

  /* Highlighted, today, and event day styles */
  .highlighted {
    background-color: rgba(166, 192, 254, 0.5); /* Transparent highlighted day color */
  }

  .today {
    background-color: rgba(255, 182, 193, 0.5); /* Transparent today's color */
  }

  .eventDay {
    background-color: rgba(255, 215, 0, 0.5); /* Transparent event day color */
  }
  .glass-effect {
    padding: 8px;
    border-radius: 4px;
    border: 1px solid rgba(255, 255, 255, 0.5); /* Transparent border */
    margin-right: 10px;
    background-color: rgba(255, 255, 255, 0.3); /* Transparent background */
    backdrop-filter: blur(5px); /* Adding blur effect */
  }
  
  /* Styling for the calendar background image */
  .calendar-container table {
    width: 450px;
    height: 450px;
    border-collapse: collapse;
    margin-top: 15px;
    backdrop-filter: blur(5px); /* Adding blur effect */
    border-radius: 4px; /* Rounded corners */
    border: 1px solid rgba(255, 255, 255, 0.3); /* Transparent border */
    background-size: cover;
    background-repeat: no-repeat;
    position: relative;
  }
  
  @import 'https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css';
  @import url('https://fonts.googleapis.com/css?family=Work+Sans:100,200,300,400,500,600,700,800,900');
  @import '../../assets/css/open-iconic-bootstrap.min.css';
  @import '../../assets/css/animate.css';
  
  @import '../../assets/css/owl.theme.default.min.css';
  @import '../../assets/css/magnific-popup.css';
  @import '../../assets/css/aos.css';
  @import '../../assets/css/ionicons.min.css';
  
  @import '../../assets/css/flaticon.css';
  @import '../../assets/css/icomoon.css';
  @import '../../assets/css/style.css';
  </style>