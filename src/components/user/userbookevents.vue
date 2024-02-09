<template>
  <div style="height:100%;">
    <br>
    
    <div class="hero-wrap hero-wrap-2 js-fullheight" style="height:1400px;" data-stellar-background-ratio="0.5">
      <div style="width: 600px; position: absolute; margin-left: 100px;">
        <div >
          <br>
          <br>
          <br>
          <br>
          <br>
          <h1 class="text-center" style=" opacity: 0; /* Set initial opacity to 0 for fade-in effect */
    animation: fade-up 0.8s ease-out forwards;font-size: 20px; font-weight:900; margin-left:50px; margin-top:50px;">BOOK YOUR <span style="font-size: 30px; font-weight:100;">|</span>&nbsp;&nbsp; <span style="font-size:70px; font-weight:400; font-family: 'WindSong', cursive;">Events...</span></h1>
          <br>
          <div>


            <button
            v-for="(item, index) in servinfo"
            :key="index"
            @click="openDialog(item)"
            type="button"
            class="neumorphic-button"
            style="
              opacity: 0;
              animation: fade-up 0.8s ease-out forwards;
              animation-delay: 0.2s;
              background-color: rgb(255, 255, 255);
              width: 260px;
              height: 100px;
              margin-left: 40px;
              margin-top: 20px;
            "
          >
            <div>
              <img
                :src="item.image"
                alt="Service Image"
                v-if="item.image"
                style="
                  box-shadow: 3px 2px 2px rgba(0, 0, 0, 0.2);
                  border-radius: 5px;
                  width: 80px;
                  margin-left: -158px;
                  margin-bottom: 10px;
                "
              />
              <span
                style="
                  position: absolute;
                  margin-left: 24px;
                  margin-top: 2px;
                  font-size: 11px;
                  font-weight: 700;
                  text-align: left;
                  font-family: 'Audiowide', cursive; 
                "
              >{{ item.service }}</span>
              <span style="display:none;">{{ item.id }}</span>
              <span
                style="
                  position: absolute;
                  margin-left: 80px;
                  font-size: 12px;
                  margin-top: 60px;
                  color: orange;
                "
              >Click here</span>
            </div>
          </button>



                
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
  </div>
  
            
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






                <!-- booking dialog-->
<v-dialog v-model="dialogs" max-width="500px">
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
</v-dialog>



  </template>
  
  
  <script>
  import axios from 'axios'

  export default {
  data() {
    return {
      servinfo: [],
      dialogs: false,
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
  
  methods: {
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