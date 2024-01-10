<template>

    <div style="position: absolute; margin-top:160px; margin-left:90px; ">
      <img style="width:70px; height:70px; "  v-if="info.length > 0" :src="info[0].profile_picture" alt="Profile" class="profile-picture-navbar">
      <span v-if="info.length > 0">
        <a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{{ info[0].username }}</a><br>
        <a style="position:absolute; margin-top:30px; text-decoration: none; color: black;" href="#"><i class="fas fa-pencil-alt"></i>&nbsp;&nbsp;&nbsp; Edit Profile</a><br>
        <a style="position:absolute; margin-top:30px; text-decoration: none; color:rgb(0, 0, 0);" href="/orderhistory"><i class="fas fa-history custom-icon"></i>&nbsp;&nbsp;&nbsp; Order History</a><br>
        <a style="position:absolute; margin-top:30px; text-decoration: none; color: black;" href="/toship_main"> <i class="fas fa-shopping-bag"></i>&nbsp;&nbsp;&nbsp; My Purchase</a><br>
        <a style="position:absolute; margin-top:30px; text-decoration: none; color: darkorange;" href="/addtocart"> <i class="fas fa-shopping-cart custom-icon"></i>  &nbsp;&nbsp;&nbsp;Shopping Cart</a>
      </span>
    </div>
    <div>

        <div class="neumorphic-search" style="margin-top: 170px; margin-left:315px; ">
            <input type="text" placeholder="Search Product by name..." class="search-input" style="border: 0px;"/>
            <button style="position:absolute; margin-left:602px; width:49px; height: 49px; " class="search-button">
                <i class="fas fa-search"></i>
              </button>
              <a href="/addtocart" style="position:absolute; margin-left:660px; width:49px; height: 49px; color: black;"  class="search-button">
                <i style="margin-left:7px; margin-top:8px;" class="fas fa-shopping-cart custom-icon"></i>
                </a>
             
              <!-- <img :src="require('../../../public/img/higa.gif')"  style="width: 180px; height: 150px;">     -->
          </div>
             
               
      
    
        <nav class="neumorphic-navbars" style="margin-top: 20px; width: 950px; height: 60px; margin-left: 315px; z-index: 10;">
          <!-- Replace these router-links or hrefs with methods that filter based on status -->
         

          <span class="nav-item">
            <a href="/pending_main" class="nav-link" style="font-weight:700; color:darkorange;" >Shopping Cart</a>
          </span>
          <span v-if="selectedCheckboxesComputed.length > 0" class="nav-item">
            <a @click="selectAllItems" class="nav-link" style="font-weight:400; color:rgb(0, 0, 0); margin-right:350px;">Select All</a>
          </span>

          <a style="margin-left: 190px; margin-right: 20px;" class="navbar-brand">Product | <span>Status.</span></a>
        </nav>


        <!-- empty cart container -->
        <div v-if="filteredInfos.length === 0" class="text-center" style="margin-top: 80px; margin-left:220px;">
          <img :src="require('../../../public/img/3cart.gif')" style="width: 55px; height: 55px;">
          <p style="font-weight: 600; margin-top:10px; margin-bottom:30px;">your shopping cart is empty.</p>
          <a href="/userproducts" class="neumorphic-button" style="text-decoration: none; border-radius: 3px;  width: 200px; background-color: rgb(248, 53, 53); color: white; transition: background-color 0.3s;" onmouseover="this.style.backgroundColor='darkred'" onmouseout="this.style.backgroundColor='rgb(248, 53, 53)'">
            Go Shopping Now
          </a>
          
        </div>
        <!-- end of empty cart container -->






        <!-- check out box -->
        <nav class="neumorphic-navbars checkout-box" style="position: fixed; bottom: 20px; left: 40px; width: 250px; height: 150px; z-index: 10;">
          <!-- ... (existing content) ... -->
          <div class="container">
            <div class="row">
              <div class="col-12">
                <button
                  @click="updateStatusToPending"
                  class="neumorphic-button checkout-button"
                  :disabled="!hasSelectedItems" 
                  style="background-color: green; color: white; margin-left: 35px; margin-top: 30px; width: 158px;"
                  onmouseover="this.style.backgroundColor='darkgreen'; this.style.color='white';"
                  onmouseout="this.style.backgroundColor='green'; this.style.color='white';"
                >
                  Check out
                </button>
              </div>
            </div>
            
          
            <div class="row">
              <div class="col-12">
                <span class="nav-item">
                  <h1 class="nav-link" style="font-weight:400; margin-left:35px; margin-top:20px; color:rgb(0, 0, 0);">
                    Total ({{ selectedCheckboxesComputed.length }} item): ₱{{ calculateTotalPrice() }}
                  </h1>
                </span>                        
              </div>
            </div>
          </div>
          
        
          <!-- <a style="margin-left: 190px; margin-right: 20px;" class="navbar-brand">Product | <span>Status.</span></a> -->
        </nav>
      
    </div>




                <!--products container-->
                <div>
                  <div v-for="filteredInfo in filteredInfos" :key="filteredInfo.id" class="container" style="margin-top: 20px;">
                    <input
                    type="checkbox"
                    :id="'checkbox-' + filteredInfo.id"
                    class="product-checkbox"
                    style="position: absolute; margin-top: 18px; margin-left: 220px;"
                    v-model="selectedCheckboxes"
                    :value="filteredInfo.id"
                    @change="updateSelectAllButton"
                  >
                    <nav class="neumorphic-navbars" style="width: 950px; margin-left: 200px; z-index: 10;">
                      <ul>
                        <li>
                          <br>
                          <div>
                            <asd><span style="color:rgb(13, 109, 19); margin-left:580px;"><i class="fas fa-box custom-icon"></i>
                              &nbsp;&nbsp;&nbsp;We will be packing your parcel soon...</span></asd>
                          </div>
            
                          <div style="margin-bottom: 20px;"> 
                            <an  v-if="filteredInfo.image">
                              <img :src="filteredInfo.image" class="img-fluids" style="max-width: 140px; max-height: 140px;" readonly>
                              <span style="margin-right: 140px; margin-left: 80px;">Product:{{ filteredInfo.prod_name }}</span> 
                              <span style="margin-right: 140px;">Quantity:{{ filteredInfo.quantity }}</span> 
                              <span >Total: ₱{{ filteredInfo.total }}</span>
                              <span v-if="!hideStatus" class="product-info">{{ status }}</span> 
                              <span v-if="!hideToken" class="product-info">{{ token }}</span>
                              <span v-if="!hideCategory" class="product-info">{{ category_id }}</span>
                         
                            </an>
                            <div>
                              
                                <button @click="openDialog(filteredInfo.category_id)" class="neumorphic-button" style="margin-left:450px; width: 200px;">
                                  <i class="fas fa-search custom-icon"></i>&nbsp;&nbsp;Find Similar
                                </button> &nbsp;&nbsp;
                                
                              <!-- <button @click="buyagain(filteredInfo.id)" class="neumorphic-button" style="margin-left:450px; width: 200px;"><i class="fas fa-phone custom-icon"></i> &nbsp;&nbsp;Buy Again</button> &nbsp;&nbsp; -->
                              <button @click="deletehistory(filteredInfo.id)"   class="neumorphic-button" style="width: 200px; background-color:rgb(248, 53, 53); color:white;">
                                Delete</button>
                            </div>
                          </div>
                        </li>
                      </ul>
                    </nav>
                  </div>
                </div>
                


                <!--kelangan walo lang makikita-->
                <v-dialog v-model="dialogs" max-width="75%">
                  <v-card>
                    <v-card-title class="headline" style="margin-left: 99px;"></v-card-title>
                    <v-card-text>
                      <div class="row justify-content-center">
                        <div v-for="(product, index) in getprods.slice(0, 8)" :key="product.id" class="col-lg-3 col-md-6 mb-4">
                          <!-- Product Card -->
                          <div class="room-item text-center">
                            <img :src="product.image" alt="" style="width: 100px; height: 100px;">
                            <div class="ri-text" >
                              <h6>{{ product.prod_name }}</h6>
                              <h6 style="display: none;">{{ product.category_id }}</h6>
                              <p style="font-size: 13px;">Unit Price: ₱{{ product.unit_price }}</p>
                              <p style="font-size: 13px;"><span style="font-size: 13px;">Available Size:</span> {{ getSizeName(product.size_id) }}</p>
                              <button class="btn btn-outline-danger btn-sm" style="width: 80px; height:33px;" @click="preOrder(product)">Pre order</button>
                            </div>
                          </div>
                        </div>
                      </div>
                    </v-card-text>
                    <v-card-actions>
                      <v-btn @click="closeDialog" color="primary">Cancel</v-btn>
                      <v-btn @click="submitReason" color="primary" small>
                        Submit
                      </v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
                
              
</template>
<script>
import axios from 'axios';

export default {
  data() {
    return {  
      selectedCheckboxes: [], // Array to store IDs of selected checkboxes
      showSelectAllButton: false, // Control visibility of a button
      originalProds: [],
      getprods: [],
      sizes: [],
      size_id: '',
      isNavbarHidden: false,
      lastScrollTop: 0,
      inputValue: '',
      isActive: false,
      isProcessing: false,
      infos: [],
	    info: [],
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
      selectedReason: null,
      selectedInfo: null,
      
    };
  },
  mounted() {
	this.getInfo(); 
  this.getOrder();
  this.getprod();

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
  hasSelectedItems() {
      return this.selectedCheckboxes.length > 0;
    },
  selectedCheckboxesComputed() {
    return this.selectedCheckboxes;
  },
  filteredInfos() {
      // Filter the 'infos' array based on the token in session storage and status equals 'Approved'
      return this.infos.filter(info => info.token === this.token && info.status === 'cart');
    },

    selectedCheckboxesComputed() {
      return this.selectedCheckboxes;
    },
  },
  methods: {
    async updateStatusToPending() {
    try {
      const confirmed = window.confirm('Are you sure you want to proceed with the checkout?');

      if (confirmed) {
        // Loop through the selectedCheckboxes array and update the status of selected items to 'pending'
        for (const id of this.selectedCheckboxes) {
          const response = await axios.post(`/updateOrderStatus/${id}`, {
            status: 'pending',
          });

          if (response.status === 200) {
            // You might want to update the UI or perform other actions upon successful update
            console.log(`Item with ID ${id} status updated to pending`);
          } else {
            console.error(`Error updating status for item with ID ${id}`);
          }
        }

        // Clear the selectedCheckboxes array after updating the status
        this.selectedCheckboxes = [];
        this.getOrder(); 
      } else {
        console.log('Checkout canceled');
      }
    } catch (error) {
      console.error('Error during checkout:', error);
    }
  },

    calculateTotalPrice() {
    let totalPrice = 0;
    this.filteredInfos.forEach(info => {
      if (this.selectedCheckboxes.includes(info.id)) {
        totalPrice += parseFloat(info.total); // Assuming 'info.total' holds the item's price
      }
    });
    return totalPrice.toFixed(2); // To display the total price with 2 decimal places
  },
    updateSelectAllButton() {
      // Check if at least one checkbox is selected
      this.showSelectAllButton = this.selectedCheckboxes.length > 0;
    },
    selectAllItems() {
      if (this.filteredInfos.length === this.selectedCheckboxes.length) {
        // If all checkboxes are already checked, uncheck all
        this.selectedCheckboxes = [];
      } else {
        // Otherwise, check all checkboxes
        this.selectedCheckboxes = this.filteredInfos.map(info => info.id);
      }

      // Call the method to update the 'Select All' button visibility
      this.updateSelectAllButton();
    },
   async deletehistory(id) {
  try {
    const confirmed = window.confirm('Are you sure you want to delete this record?');

    if (confirmed) {
      const userInput = prompt('Type "okay" to confirm:');
      if (userInput && userInput.trim().toLowerCase() === 'okay') {
        const response = await axios.post(`/deleteprod/${id}`, {
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

openDialog(categoryId) {
      this.dialogs = true; // Open the dialog

      // Filter products based on category_id from originalProds
      this.getprods = this.originalProds.filter(
        (product) => product.category_id === categoryId
      );
    },  

    closeDialog() {
      this.dialogs = false; // Close the dialog
    },
    async getOrder() {
  try {
    const response = await axios.get('getOrder');
    this.infos = response.data;
    // Set hideToken to true after fetching notifications
    this.hideToken = true;
  } catch (error) {
    console.error(error);
  }
},
async getprod() {
      try {
        const response = await axios.get('getprod');
        this.getprods = response.data;
        this.originalProds = [...response.data]; // Store original products
        // Set hideToken to true after fetching notifications
        this.hideToken = true;
      } catch (error) {
        console.error(error);
      }
    },
getSizeName(sizeId) {
      const size = this.sizes.find(size => size.size_id === sizeId);
      return size ? size.item_size : 'Unknown';
    },
    async getItemSizes() {
      try {
        const response = await axios.get('getsize');
        this.sizes = response.data;
      } catch (error) {
        console.log(error);
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

<style>

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

/* Navbar link hover styles */
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
</style>
