<template>

    <div style="position: absolute; margin-top:160px; margin-left:90px; ">
      <img style="width:70px; height:70px; "  v-if="info.length > 0" :src="info[0].profile_picture" alt="Profile" class="profile-picture-navbar">
      <span v-if="info.length > 0">
        <a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{{ info[0].showed_username }}</a><br>
        <a style="position:absolute; margin-top:30px; text-decoration: none; color: darkorange;" href="/editprofiles"><i class="fas fa-pencil-alt"></i>&nbsp;&nbsp;&nbsp; Edit Profile</a><br>
        <a style="position:absolute; margin-top:30px; text-decoration: none; color:black;" href="/orderhistory"><i class="fas fa-history custom-icon"></i>&nbsp;&nbsp;&nbsp; Order History</a><br>
        <a style="position:absolute; margin-top:30px; text-decoration: none; color: black;" href="/toship_main"> <i class="fas fa-shopping-bag"></i>&nbsp;&nbsp;&nbsp; My Purchase</a>
        <br>
        <a style="position:absolute; margin-top:30px; text-decoration: none; color: rgb(0, 0, 0);" href="/addtocart"> <i class="fas fa-shopping-cart custom-icon"></i>  &nbsp;&nbsp;&nbsp;Shopping Cart</a>
      </span>
    </div>
    <div>

        <!-- <div class="neumorphic-search" style="margin-top: 170px; margin-left:315px;">
            <input type="text" placeholder="Search Product by name..." class="search-input" style="border: 0px;"/>
            <button style="position:absolute; margin-left:602px; width:49px; height: 49px; " class="search-button">
                <i class="fas fa-search"></i>
              </button>
          </div> -->
             
               
      
    
        <nav class="neumorphic-navbars" style="margin-top: 150px; width: 950px; height: 60px; margin-left: 315px; z-index: 10;">
          <!-- Replace these router-links or hrefs with methods that filter based on status -->
         

          <span class="nav-item">
            <a href="/editprofiles" class="nav-link" style="font-weight:700; color:darkorange; margin-right:350px;" >Edit Profile</a>
          </span>

          <a style="margin-left: 190px; margin-right: 20px;" class="navbar-brand">Edit | <span>Profile.</span></a>
        </nav>
      
    </div>




                <!--products container-->
                <div>
                  <div class="container" style="margin-top: 20px;">
                    <nav class="neumorphic-navbars" style="width: 945px; margin-left: 200px; z-index: 10;">
                      <ul>
                        <li>
                          <br>
                          <div>
                            
                          </div>
            
                          <div class="card mb-4 mb-xl-0" style="margin-top:8px; width: 880px;">
                            <div class="card-header">Profile Picture</div>
                <div class="card-body text-center">
                    <!-- Profile picture image-->
                   
                    <img class="img-account-profile rounded-circle mb-2" v-if="selectedImage" :src="selectedImage" alt="" style="box-shadow: 10px 10px 30px #eeecec, -5px -5px 20px #ffffff;">
<img class="img-account-profile rounded-circle mb-2" v-else-if="info.length > 0" :src="info[0].profile_picture" alt="" style="box-shadow: 10px 10px 30px #eeecec, -5px -5px 20px #ffffff;">
<img class="img-account-profile rounded-circle mb-2" v-else :src="'path_to_default_image.jpg'" alt="" style="box-shadow: 10px 10px 30px #eeecec, -5px -5px 20px #ffffff;">

<!-- Profile picture help block -->
<div class="small font-italic text-muted mb-4">JPG or PNG no larger than 5 MB</div>

<!-- Profile picture upload button -->
<input type="file" style="border: 0; width:29%; border-radius:5px; background-color:rgb(220, 220, 223)" class="neumorphic-button" accept="image/*" @change="updateEditImage" required>
               </div>
               </div>

              
            <!-- Account details card-->
            <div class="card mb-4" style="height:700px;">
                <div class="card-header">Account Details</div>
                <div class="card-body">
               
                        <!-- Form Group (username)-->
                        <div style="margin-left: 10px;">
                        <div class="mb-3" >
                            <label class="small mb-1" for="inputUsername">Username (how your name will appear to other users on the site)</label>
                            <input v-if="info.length > 0" class="form-control" id="inputUsername" type="text" placeholder="Enter your username" v-model="info[0].showed_username">
                        </div>
                        <!-- Form Row-->
                        <div class="row gx-3 mb-3">
                            <!-- Form Group (first name)-->
                            <div class="col-md-6">
                                <label class="small mb-1" for="inputFirstName">Contact</label>
                                <input v-if="info.length > 0" class="form-control" id="inputFirstName" type="text" placeholder="Enter your contact" v-model="info[0].contact">
                            </div>
                            <!-- Form Group (last name)-->
                            <div class="col-md-6">
                                <label class="small mb-1" for="inputLastName">Address</label>
                                <input v-if="info.length > 0" class="form-control" id="inputLastName" type="text" placeholder="Enter your Address" v-model="info[0].address">
                            </div>
                        </div>
                        <!-- Form Group (email address)-->
                        <div class="mb-3">
                            <label class="small mb-1" for="inputEmailAddress">Other Information (Delivery location or Customer information):</label>
                            <input class="form-control" id="inputEmailAddress" type="text" placeholder="Enter your other information" v-model="info[0].other_info">
                        </div>
                        <!-- Form Row-->
                        <div class="row gx-3 mb-3">
                            <!-- Form Group (phone number)-->
                            <div class="col-md-6">
                                <label class="small mb-1" for="input_name">Name</label>
                                <input class="form-control" id="input_name" type="tel" placeholder="Enter your name" v-model="info[0].legit_name">
                            </div>
                            <!-- Form Group (birthday)-->
                            <div class="col-md-6">
                              <label>
                                <a4 style="font-size: 14px;">&nbsp;&nbsp; Gender:</a4>
                              </label>
                              <br>
                              <label style="margin-top: 8px; margin-left:10px;">
                                <input type="radio" v-model="info[0].gender" value="male"> Male
                              </label>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                              
                              <label>
                                <input type="radio" v-model="info[0].gender" value="female"> Female
                              </label>    
                              
                              <div>
                                <label for="province">Province:</label>
                                <select id="province" v-model="selectedProvince" @change="onProvinceChange">
                                  <option v-for="province in provinces" :key="province.id" :value="province.id">{{ province.name }}</option>
                                </select>
                            
                                <label for="city" v-if="selectedProvince">City:</label>
                                <select id="city" v-model="selectedCity" v-if="selectedProvince" @change="onCityChange">
                                  <option v-for="city in cities" :key="city.id" :value="city.id">{{ city.name }}</option>
                                </select>
                            
                                <label for="barangay" v-if="selectedCity">Barangay:</label>
                                <select id="barangay" v-model="selectedBarangay" v-if="selectedCity">
                                  <option v-for="barangay in barangays" :key="barangay.id" :value="barangay.id">{{ barangay.name }}</option>
                                </select>
                              </div>
                            

                            </div>

                          </div>
                        </div>
                        <!-- Save changes button-->
                        <button class="btn btn-primary" style="margin-left: 350px; margin-top: 30px; width: 150px;" type="submit">Save changes</button>
              
                            </div>

                          </div>
                        </li>
                      </ul>
                      
                    </nav>
                  </div>
                </div>
            


                <!--cancel modal-->
                <v-dialog v-model="dialogs" max-width="500px">
                  <v-card>
                    <v-card-title class="headline" style="margin-left: 99px;">Reasons for Order Cancellation</v-card-title>
                    <v-card-text>
                      <v-radio-group v-model="selectedReason">
                        <v-radio v-for="(reason, index) in cancellationReasons" :key="index" :label="reason" :value="reason"></v-radio>
                      </v-radio-group>
                    </v-card-text>
                    <v-card-actions>
                      <v-btn @click="closeDialog" color="primary">Cancel</v-btn>
                      <v-btn @click="submitReason" color="primary">Submit</v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
              
</template>
<script>
import axios from 'axios';

export default {
  data() {
    return {
      selectedProvince: null,
      selectedCity: null,
      selectedBarangay: null,
      provinces: [
        { id: 1, name: 'Abra' },
  { id: 2, name: 'Agusan del Norte' },
  { id: 3, name: 'Agusan del Sur' },
  { id: 4, name: 'Aklan' },
  { id: 5, name: 'Albay' },
  { id: 6, name: 'Antique' },
  { id: 7, name: 'Apayao' },
  { id: 8, name: 'Aurora' },
  { id: 9, name: 'Basilan' },
  { id: 10, name: 'Bataan' },
  { id: 11, name: 'Batanes' },
  { id: 12, name: 'Batangas' },
  { id: 13, name: 'Benguet' },
  { id: 14, name: 'Biliran' },
  { id: 15, name: 'Bohol' },
  { id: 16, name: 'Bukidnon' },
  { id: 17, name: 'Bulacan' },
  { id: 18, name: 'Cagayan' },
  { id: 19, name: 'Camarines Norte' },
  { id: 20, name: 'Camarines Sur' },
  { id: 21, name: 'Camiguin' },
  { id: 22, name: 'Capiz' },
  { id: 23, name: 'Catanduanes' },
  { id: 24, name: 'Cavite' },
  { id: 25, name: 'Cebu' },
  { id: 26, name: 'Compostela Valley' },
  { id: 27, name: 'Cotabato' },
  { id: 28, name: 'Davao de Oro' },
  { id: 29, name: 'Davao del Norte' },
  { id: 30, name: 'Davao del Sur' },
  { id: 31, name: 'Davao Occidental' },
  { id: 32, name: 'Davao Oriental' },
  { id: 33, name: 'Dinagat Islands' },
  { id: 34, name: 'Eastern Samar' },
  { id: 35, name: 'Guimaras' },
  { id: 36, name: 'Ifugao' },
  { id: 37, name: 'Ilocos Norte' },
  { id: 38, name: 'Ilocos Sur' },
  { id: 39, name: 'Iloilo' },
  { id: 40, name: 'Isabela' },
  { id: 41, name: 'Kalinga' },
  { id: 42, name: 'La Union' },
  { id: 43, name: 'Laguna' },
  { id: 44, name: 'Lanao del Norte' },
  { id: 45, name: 'Lanao del Sur' },
  { id: 46, name: 'Leyte' },
  { id: 47, name: 'Maguindanao' },
  { id: 48, name: 'Marinduque' },
  { id: 49, name: 'Masbate' },
  { id: 50, name: 'Misamis Occidental' },
  { id: 51, name: 'Misamis Oriental' },
  { id: 52, name: 'Mountain Province' },
  { id: 53, name: 'Negros Occidental' },
  { id: 54, name: 'Negros Oriental' },
  { id: 55, name: 'Northern Samar' },
  { id: 56, name: 'Nueva Ecija' },
  { id: 57, name: 'Nueva Vizcaya' },
  { id: 58, name: 'Occidental Mindoro' },
  { id: 59, name: 'Oriental Mindoro' },
  { id: 60, name: 'Palawan' },
  { id: 61, name: 'Pampanga' },
  { id: 62, name: 'Pangasinan' },
  { id: 63, name: 'Quezon' },
  { id: 64, name: 'Quirino' },
  { id: 65, name: 'Rizal' },
  { id: 66, name: 'Romblon' },
  { id: 67, name: 'Samar' },
  { id: 68, name: 'Sarangani' },
  { id: 69, name: 'Siquijor' },
  { id: 70, name: 'Sorsogon' },
  { id: 71, name: 'South Cotabato' },
  { id: 72, name: 'Southern Leyte' },
  { id: 73, name: 'Sultan Kudarat' },
  { id: 74, name: 'Sulu' },
  { id: 75, name: 'Surigao del Norte' },
  { id: 76, name: 'Surigao del Sur' },
  { id: 77, name: 'Tarlac' },
  { id: 78, name: 'Tawi-Tawi' },
  { id: 79, name: 'Zambales' },
  { id: 80, name: 'Zamboanga del Norte' },
  { id: 81, name: 'Zamboanga del Sur' },
  { id: 82, name: 'Zamboanga Sibugay' }
      ],
      cities: [
        { id: 1, name: 'Quezon City', provinceId: 1 },
        // Add other cities
      ],
      barangays: [
        { id: 1, name: 'Barangay 1', cityId: 1 },
        // Add other barangays
      ],

      selectedGender: '',
      selectedImage: null,
        isNavbarHidden: false,
      lastScrollTop: 0,
      inputValue: '',
      isActive: false,
      isProcessing: false,
      infos: [],
	    info: [ {
          profile_picture: 'path_to_default_image.jpg',
          // other properties...
        }],
      token: '',
      status: '',
      dialogs: false,
      selectedReason: null,
      cancellationReasons: [
        'Need to change delivery address',
        'Seller is not responsive to my inquiries',
        'Others/Change of mind'
        // Add more reasons if needed
      ],
      hideStatus: false,
      selectedInfo: null,
      
    };
  },
  mounted() {
	this.getInfo(); 
  this.getOrder();
  },
  created() {
	this.token = sessionStorage.getItem('jwt');
  if (this.token) {
    this.getInfo();
  } else {
    // Handle the case where token is not available in local storage
    console.error('JWT token not found in local storage');
  }
  this.getInfo();
},
  computed: {
    filteredProducts() {
      // Filter products based on the status
      return this.infos.filter(product => product.status !== 'deleted');
    },
  },

  methods: {

    onProvinceChange() {
      this.selectedCity = null;
      this.selectedBarangay = null;
    },
    onCityChange() {
      this.selectedBarangay = null;
    },
    updateEditImage(event) {
    // Get the selected file from the input
    const file = event.target.files[0];

    // Check if a file is selected
    if (file) {
      // Display the selected image
      this.selectedImage = URL.createObjectURL(file);
      
      // You can also send the file to the server for processing if needed
      // Example: this.uploadImageToServer(file);
    }
  },
   async deletehistory(id) {
  try {
    const confirmed = window.confirm('Are you sure you want to delete this record?');

    if (confirmed) {
      const userInput = prompt('Type "okay" to confirm:');
      if (userInput && userInput.trim().toLowerCase() === 'okay') {
        const response = await axios.post(`/updateNotifStatus/${id}`, {
          status: 'deleted',
        });

        if (response.status === 200) {
          this.getOrder(); // Refresh orders after status update
        } else {
          console.error('Error updating order status');
        }
      } else {
        console.log('No changes were made.');
      }
    } else {
      console.log('No changes were made.');
    }
  } catch (error) {
    console.error('Error updating order status:', error);
  }
},
    openDialog() {
      this.dialogs = true;
    },
    closeDialog() {
      this.dialogs = false;
      this.selectedReason = null; // Reset selected reason
    },
    submitReason() {
      // Handle submission of selected reason, e.g., emit an event or perform an action
      if (this.selectedReason) {
        // Perform action with selected reason
        console.log('Selected Reason:', this.selectedReason);
        // Reset selected reason and close dialog
        this.selectedReason = null;
        this.dialog = false;
      } else {
        // Inform user to select a reason
        console.log('Please select a reason.');
        // Optionally, you can provide a message to the user indicating they need to select a reason before submitting.
      }
    },
    async getOrder() {
  try {
    const response = await axios.get('getNotif');
    this.infos = response.data;
    // Set hideToken to true after fetching notifications
    this.hideToken = true;
  } catch (error) {
    console.error(error);
  }
},
    toggleDropdown() {
    const menu = document.querySelector('.menu-item');
    menu.classList.toggle('active');
  },
  async getInfo() {
    try {
      const response = await axios.get(`getUserData/${this.token}`);
      this.info = response.data; // Assuming response.data is an object/array of user data
    } catch (error) {
      console.error(error);
      // Handle the error case, such as showing a message to the user
    }
  },
  handleScroll() {
      const currentScroll = window.pageYOffset || document.documentElement.scrollTop;

      if (currentScroll <= 0) {
        // At the top of the page
        this.isNavbarHidden = false;
      } else {
        // Scrolled down
        this.isNavbarHidden = true;
      }

      this.lastScrollTop = currentScroll <= 0 ? 0 : currentScroll;
    },
    activateFinder() {
      this.isActive = true;
    },
    deactivateFinder() {
      if (this.inputValue.length === 0) {
        this.isActive = false;
      }
    },
    submitForm() {
      this.isProcessing = true;
      this.isActive = false;
      this.$refs.icon.classList.remove('active');
      this.$refs.icon.classList.add('processing');
      this.inputValue = ''; // Clear input value

      setTimeout(() => {
        this.isProcessing = false;
        this.$refs.icon.classList.remove('processing');
        this.inputValue = ''; // Clear input value again

        if (this.inputValue.length > 0) {
          this.isActive = true;
          this.$refs.icon.classList.add('active');
        }
      }, 1000);
    },
  }
};
</script>

<style scoped>
.button-container {
  display: flex;
}
.active {
  background-color: lightblue;
}
.neumorphic-navbars {

  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 10px 10px 30px #eeecec, -10px -10px 30px #ffffff;
  transition: top 0.3s;
}
.neumorphic-navbars a {
  color: rgb(14, 13, 13)262;
  text-decoration: none;
  padding: 8px 15px;
  border-radius: 3px;
  transition: all 0.3s ease;
}

/* Navbar link hover style=scope's */
.neumorphic-navbars a:hover {
  background-color: #e9e1e1;
  box-shadow: 5px 5px 10px #bcbcbc, -5px -5px 10px #ffffff;
  color: #1b1b1b;
}

a[href="#"] {
  text-decoration: none;
  color: black;
}

.neumorphic-search {
    display: flex;
    align-items: center;
    border-radius: 5px;
    background-color: #fff;
    box-shadow: 10px 10px 30px #eeecec, -10px -10px 30px #ffffff;
    padding: 8px;
    height: 40px;
    margin-top: 35px; /* Adjust this margin as needed */
    margin-left: 70px; /* Adjust this margin as needed */
    width: 600px;
  }

  .search-input {
    height: 36px;
    margin-top: 2px;
    border: none;
    outline: none;
    flex: 1;
    padding: 8px;
    border-radius: 5px;
    box-shadow: inset 2px 2px 5px #c9c9c9, inset -2px -2px 5px #ffffff;
  }

  .search-button {
    background-color: #fff;
    border: none;
    outline: none;
    cursor: pointer;
    padding: 8px;
    border-radius: 5px;
    margin-left: 8px;
    margin-bottom: 12px;
    width: 40px;
    box-shadow: 3px 3px 10px rgba(0, 0, 0, 0.1);
  }
  body{margin-top:20px;
background-color:#f2f6fc;
color:#69707a;
}
.img-account-profile {
    height: 10rem;
}
.rounded-circle {
    border-radius: 50% !important;
}
.card {
    box-shadow: 0 0.15rem 1.75rem 0 rgb(33 40 50 / 15%);
}
.card .card-header {
    font-weight: 500;
}
.card-header:first-child {
    border-radius: 0.35rem 0.35rem 0 0;
}
.card-header {
    padding: 1rem 1.35rem;
    margin-bottom: 0;
    background-color: rgba(33, 40, 50, 0.03);
    border-bottom: 1px solid rgba(33, 40, 50, 0.125);
}
.form-control, .dataTable-input {
    display: block;
    width: 100%;
    padding: 0.875rem 1.125rem;
    font-size: 0.875rem;
    font-weight: 400;
    line-height: 1;
    color: #69707a;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #c5ccd6;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    border-radius: 0.35rem;
    transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.nav-borders .nav-link.active {
    color: #0061f2;
    border-bottom-color: #0061f2;
}
.nav-borders .nav-link {
    color: #69707a;
    border-bottom-width: 0.125rem;
    border-bottom-style: solid;
    border-bottom-color: transparent;
    padding-top: 0.5rem;
    padding-bottom: 0.5rem;
    padding-left: 0;
    padding-right: 0;
    margin-left: 1rem;
    margin-right: 1rem;
}
</style>