<template>
    <Menu />
    <button @click="opendialog" class="neumorphic-button" style="position:absolute; width:170px; left:83%;">ADD EVENT</button>
    <br>
    <div class="row" style="margin-left: 300px; margin-right: 20px;">
        <div class="col-md-12 col-sm-12">
              <h2>List of Services</h2>
            </div>
              <div class="row">
                <div class="col-sm-12">
                  <div class="card-box table-responsive">
                      <insert @data-saved="getInfo" />
                    <table id="datatable-responsive" class="table table-bordered table-striped dt-responsive nowrap" cellspacing="0" width="80%" style="margin: 0 auto;">
                      <thead>
                        <tr>
                          <th>ID</th>
                          <th>IMAGE</th>
                          <th>SERVICE</th>
                          <th>INFORMATION</th>
                          <th>LOWEST PRICE</th>
                          <th>HIGHEST PRICE</th>
                          <th>ACTION</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for="info in info">
                          <td>{{ info.id}}</td>
                          <td>
                            <img v-if="info.image" :src="info.image" alt="Image" style="width:100px; height:100px;">
                            <span v-else>No Image</span>
                          </td>
                          <td>{{ info.service}}</td>
                          <td>{{ info.information}}</td>
                          <td>{{ info.low_pricing}}</td>
                          <td>{{ info.high_pricing}}</td>
                          <td>
                            <button @click="editRecord" class="btn btn-success btn-sm edit"> EDIT</button>
                          </td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                </div>
              </div>
            </div>


            <v-dialog v-model="dialogss" max-width="500px">
                <form @submit.prevent="saveBooking" class="container">
                  <v-card>
                    <br>
                    <v-card-title class="headline" style="margin-left: 155px; font-size: 14px; font-weight:900;  ">ADD<span style="font-size: 22px;  font-weight:100;">&nbsp;&nbsp;|&nbsp;</span><span style="font-weight:400; font-family: 'WindSong', cursive; font-size:33px;">Services</span></v-card-title>
                    <v-card-text>
              
                      <div class="form-group">
                        <label for="service_title">Service Title:</label>
                        <input type="text" class="search-input" style="width:100%; height:45px;" placeholder="Service Title" v-model="service" required>
                      </div>
                      <br>
                      <div class="form-row">
                        <div class="form-group col-md-6">
                          <label for="file_upload">Upload File:</label>
                          <input type="file" id="file_upload" class="neumorphic-button" style="width: 110%; background-color: white; border-radius: 3px;" @change="handleFileChange" accept="image/*" required>
                        </div>
                        <div>
                          <img v-if="imageUrl" :src="imageUrl" alt="Uploaded Image" style="position:absolute;width: 120px; height: 120px; right:11%;">
                        </div>
                      </div>
                      
                      
                      <br><br>
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
  import { defineComponent } from 'vue';
  import axios from 'axios'
  import Menu from '@/components/admin/Menu.vue'
  
  export default
  defineComponent({
    data() {
    return { 
      info: [], 
      dialogss: false,
      imageUrl: null,
    }
  },
      components:{
          Menu,
          info:[],

      },
      created(){
          console.log(Menu);
          this.getInfo();
      },
      methods: {
        async getInfo() {
      try {
        const response = await axios.get('getservice');
        this.info = response.data;
      } catch (error) {
        console.error(error);
      }
    }, 
    handleFileChange(event) {
      const file = event.target.files[0];
      if (file) {
        this.imageUrl = URL.createObjectURL(file);
      }
    },
    opendialog(){
        this.dialogss = true;
      },
      closemodal(){
        this.dialogss = false;
      },
      }
  });
  </script>
  
  <style>
  
  </style>
  
  
  