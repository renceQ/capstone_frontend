  <template>
    <nav
    class="neumorphic-navbar"
    style="border-radius: 5px; height: 475px; width: 450px; overflow-y: auto;
           display: flex; flex-direction: column; justify-content: flex-start;
           align-items: flex-start; margin-top: 60px; margin-left: 15%;"
  >

  <div v-for="product in products" :key="product.product_id" style="width: 350px; margin-left:20px; margin-top:10px;">
  
    <img style="width:50px; height:50px; margin-bottom:15px; margin-top:3px;" v-if="info.length > 0" :src="product.profile_picture" alt="Profile" class="profile-picture-navbar">
    
    <span style="font-weight:900;" v-if="info.length > 0 && product.isAnonymous === 'anonymous'">&nbsp;&nbsp; &nbsp;&nbsp;******</span>
    <span style="position:absolute; margin-top:15px;font-family: 'Sacramento', cursive; font-weight:600; font-size:22px;" v-else>&nbsp;&nbsp; &nbsp;&nbsp;{{ product.username }}</span>
  
    <p>ordered item: {{ product.prod_name }}</p>
    <p>Comment:</p>
    <p>{{ product.comment }}</p>
    <!-- Add other fields as needed -->
    <img v-if="product.first_image" style="height:100px; width:100px;margin-right:10px;" :src="product.first_image" />
    <img v-if="product.second_image" style="height:100px; width:100px;margin-right:10px;" :src="product.second_image" />
    <img v-if="product.third_image" style="height:100px; width:100px;" :src="product.third_image" />      
    <div>
      <br>
      <p style="display: none;">Product ID: {{ product.product_id }}</p>
      <p style="display: none;">Rate: {{ product.rate }}</p>
      <div v-if="product.rate === 'Bad'">
        
        <p>Rate:&nbsp;&nbsp;<span style="color: yellow; font-size:20px;">★ &nbsp;&nbsp;<span style="color: black; font-size:14px;">Bad</span></span></p>
      </div>
      <div v-else-if="product.rate === 'Poor'">
        
        <p> Rate:&nbsp;&nbsp;<span style="color: yellow; font-size:20px;">★★ &nbsp;&nbsp;<span style="color: black; font-size:14px;">Poor</span></span></p>
      </div>
      <div v-else-if="product.rate === 'Average'">
   
        <p> Rate:&nbsp;&nbsp;<span style="color: yellow; font-size:20px;">★★★ &nbsp;&nbsp;<span style="color: black; font-size:14px;">Average</span></span></p>
      </div>
      <div v-else-if="product.rate === 'Great'">
       
        <p> Rate:&nbsp;&nbsp;<span style="color: yellow; font-size:20px;">★★★★ &nbsp;&nbsp;<span style="color: black; font-size:14px;">Great</span></span></p>
      </div>
      <div v-else-if="product.rate === 'Excellent'">
       
        <p> Rate:&nbsp;&nbsp;<span style="color: yellow; font-size:20px;">★★★★★ &nbsp;&nbsp;<span style="color: black; font-size:14px;">Excellent</span></span></p>
      </div>
      <p style="display: none;">Anonymous: {{ product.isAnonymous }}</p>
    </div>
    <hr />
  </div>
  
    <router-link
    to="#"
    @click="toggleReviews"
    style="position: fixed; bottom: 100px; left: 465px; width:150px; font-size: 14px; font-weight: 200; font-size: 11px; background-color: green; color: rgb(255, 255, 255)"
    class="neumorphic-button">
    &nbsp;&nbsp; &nbsp;&nbsp; PRODUCT INFO
</router-link>


    
  </nav>

 
  <br>
    <div class="container mt-4" style="margin-left:270px; height:200px;">
      <h2 style="margin-left:450px; font-size:25px; margin-top:70px; ">ORDER FORM</h2>
      <form @submit.prevent="placeOrder">
      <div class="row">
        <div class="col">
          <div style="display: none;">
            <p>Image:</p>
            <img :src="productData.image" alt="Product Image" class="img-fluid" style="max-width: 200px; max-height: 200px;">
            <p>Product Name: <a style="font-size: 10px;">{{ productData.prod_name }}</a></p>
            <p>Unit Price: ₱{{ productData.unit_price }}</p>
            <p>size : {{ getSizeName(productData.size_id) }}</p>
        </div>
          <div class="mb-3">
            <p>Quantity:</p>
            <div class="btn-group" role="group" aria-label="Quantity">
              <button @click="decreaseQuantity" type="button" class="btn btn-secondary" style="height:38px;">-</button>
              <p class="btn btn-secondary">{{ quantity }}</p>
              <button @click="increaseQuantity" type="button" class="btn btn-secondary" style="height:38px;">+</button>
            </div>
            </div>
            <!--hidden fields-->
            <input type="hidden" v-model="productData.id">
            <input type="hidden" v-model="productData.category_id">
            <input type="hidden" v-model="productData.transaction_code">

            <div>
              <h5 >CONTACT DETAILS</h5>
              <div style="margin-top: 20px;">
                <div v-for="userData in info" :key="userData.id" class="user-profile">
                  <div class="profile-details">
                    <div class="row">
                      <div class="col-sm-6">
                          
                        Address:<input type="text" v-model="userData.address" placeholder="Enter Address" class="search-input" style="border: 0px;" required>
                      </div>
                      <div class="col-sm-6">
                        Contact:<input type="text" v-model="userData.contact" placeholder="Enter Contact" class="search-input" style="margin-left:90px; border: 0px;" required>
                      </div>
                    </div>
                    <div class="row">
                      <div class="col-sm-6">
                        Other Information: <input type="text" v-model="userData.other_info" placeholder="Enter Other Information"  class="search-input" style="border: 0px;" required>
                        <input type="hidden" v-model="userData.token" placeholder="Enter Other Information"  class="search-input" style="border: 0px;" required>
                    </div>
                    <div class="col-sm-6">
                                          <!-- <label for="customerName">Customer Name:</label> -->
                      <p>Username:</p><input  type="text" id="customerName" v-model="userData.username" placeholder="customer name"  class="search-input" style="border: 0px; margin-left:90px;" required>
                  </div>
                    </div>
                    
                    <div>

                      <a style="position: absolute; margin-left:120px; margin-top:8px;">Total Price: ₱</a>
                      <input type="text" style="border:0px;  position: absolute;margin-left:192px;" v-model="productData.total" placeholder="total price" disabled> 
                    </div>
                  </div>
                </div>
                
              
              </div>
            </div>

          <div >
            <br>
            <br>
            <div class="row">
              <button1 @click="opendialog"  style=" border-radius:5px; width:32%; width:220px; margin-right:2%; margin-bottom:3%; " class="neumorphic-button">&nbsp;&nbsp;<i class="fas fa-credit-card custom-icon"></i>&nbsp;&nbsp;Select Payment Method</button1>
              <div class="row">
            <button1 @click="placeOrder('cart')" type="submit" style=" border-radius:5px; width:24%;  margin-right:2%; margin-bottom:3%; " class="neumorphic-button">&nbsp;&nbsp;<i class="fas fa-shopping-cart custom-icon"></i>&nbsp;&nbsp;Add to Cart</button1>
            <button1 @click="placeOrder('pending')" type="submit" style="  border-radius:5px;width:24%;  margin-bottom:3%;" class="neumorphic-button">&nbsp;&nbsp;<i class="fas fa-shopping-bag custom-icon"></i>&nbsp;&nbsp;Place Order</button1>
          </div>

            
            </div>
          </div>
          </div>
        </div>
      </form>
      </div>

      <v-dialog v-model="dialog" persistent max-width="400">
        <v-card>
          <v-card-text>
            <div class="text-center">
              <p>  Your order has been successfully placed. </p>
              <img :src="require('../../../public/img/check.gif')"  style="width: 120px; height: 120px;">
            </div>
          </v-card-text>
          <v-card-actions>
            <v-btn  style="margin-left:162px;"  href="/userproducts" color="primary" @click="dialog = false">OK</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>

      <v-dialog v-model="dialogs" persistent max-width="400">
        <v-card>
          <v-card-text>
            <div class="text-center">
              <p>  Your order has been successfully added to cart. </p>
              <img :src="require('../../../public/img/dash.gif')"  style="width: 180px; height: 150px;">
            </div>
          </v-card-text>
          <v-card-actions>
            <v-btn  style="margin-left:162px;"  href="/userproducts" color="primary" @click="dialog = false">OK</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
      

      <v-dialog v-model="dialogss" persistent max-width="400">
        <v-card>
          <v-card-text>
            <div class="text-center">
              <p>  Choose payment method </p>
              <!-- <img :src="require('../../../public/img/dash.gif')"  style="width: 180px; height: 150px;"> -->
            <!-- add payment button here -->
            <a class="neumorphic-navbars" style="width: 150px; border-radius:17px; margin-left:96px;" href="https://connect-sb-issuing.paymaya.com/login" target="_blank">
              <img src="https://payments-web-sbx-assets.maya.ph/payments-web/assets/static/media/pay-with-maya.a7968dfe.svg" alt="Paymaya" style="width: 150px; height: 50px;">
            </a>  
            </div>
          </v-card-text>
          <v-card-actions>
            <v-btn  style="margin-left:162px;"   color="primary" @click="closemodal">OK</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>


      <div v-if="!showReviews" >
        <nav
        class="neumorphic-navbar"
        style="border-radius:5px;height:483px; width: 450px; display: flex; flex-direction: column; justify-content: flex-start; align-items: flex-start; margin-top:60px; margin-left:15%;"
      >
          <p style=" margin-left: 20px; margin-bottom: 10px; font-size: 11px; font-weight:600; font-family: 'Audiowide', cursive;">PRODUCT NAME:  <span style="font-size: 30px; font-weight:400; margin-left:15px; color:rgb(223, 146, 5);font-family: 'Sacramento', cursive;">{{ productData.prod_name }}</span></p> 
      
          <div style="display: flex; flex-direction: column; align-items: center; margin-bottom: 20px;">
              <!-- <p>Image:</p> -->
              <img :src="productData.image" alt="Product Image" class="img-fluid" style="max-width: 250px; max-height: 250px; margin-top:20px; margin-left: 90px;">
          </div>
      
          <p style="margin-left: 20px; margin-bottom: 10px; font-size: 11px; font-weight:700;font-family: 'Audiowide', cursive;">UNIT PRICE: <span style="font-weight: 200; margin-left: 10px; color:rgb(240, 141, 29); font-size:20px; font-family: 'Podkova', sans-serif;">₱  <span style="font-family: 'Wallpoet', cursive; font-weight:200;font-size:30px; color:rgb(240, 141, 29);">{{ productData.unit_price }}</span></span></p>
          <p style="margin-left: 20px; margin-bottom: 10px; font-size: 11px; font-weight:600;font-family: 'Audiowide', cursive;" >SIZE: <span style="margin-left: 10px; color:rgb(240, 141, 29);font-weight:100; font-size:16px;">{{ getSizeName(productData.size_id) }}</span></p>
          <p style="margin-left: 20px; margin-bottom: 15px; font-size: 11px; font-weight:600;font-family: 'Audiowide', cursive;" >SHARE: <span style="margin-left: 10px; font-size:20px; "><i class="fab fa-facebook custom-icon"></i>&nbsp;&nbsp;<i class="fab fa-instagram custom-icon"></i>&nbsp;&nbsp;<i class="fab fa-twitter custom-icon"></i>&nbsp;&nbsp;<i class="fab fa-facebook-messenger custom-icon"></i></span></p>
          <router-link
        to="#"
        @click="toggleReviews"
        style="position: absolute; bottom: 114px; width: 150px; right: 35px; font-size: 14px; font-weight: 200; font-size: 11px; background-color:green; color: rgb(255, 255, 255)"
        class="neumorphic-button"
      >
        &nbsp;&nbsp;PRODUCT REVIEWS
      </router-link>
      <router-link
      to="#"
      @click="toggleReviews"
      style="position: absolute; bottom: 74px; width: 150px; right: 35px; height:31px; font-size: 9.5px; font-weight: 200;  background-color:#868686; color: rgb(255, 255, 255)"
      class="neumorphic-button"
    >
      &nbsp;&nbsp;PRODUCT DESCRIPTION
    </router-link>
          <router-link to="/userproducts" style=" border-radius:5px;width:150px; margin-left:250px; position:absolute; margin-top:402px; font-size:10px; font-weight:500; background-color:rgb(19, 18, 18);color:rgb(255, 255, 255)" class="neumorphic-button">  CHOOSE ANOTHER PRODUCT</router-link>
          
      </nav>
    </div>
  

      
  </template>

  <script>
  import axios from 'axios'

  export default {
    data() {
      return {
        products: [],
        showReviews: false,
        status: '',
        dialog: false,
        dialogs: false,
        dialogss: false,
        productData: {
          image: '',
          prod_name: '',
          unit_price: '',
          sizes: [],
          transaction_code: '',
          total: 0,
          category_id: '',

        },
        info: [],
        quantity: 1, // Initial quantity
        size_id: '',
        image:'', 
          prod_name:'', 
          unit_price:'',  
          address:'', 
          contact:'', 
          other_info:'', 
          customerName: '',
          id: '',
          token: '',
          status: '',
          username: '',
          category_id: '',
          
      };
    },
    
    created() {
      this.getProductDetails();
      this.token = sessionStorage.getItem('jwt');
      if (this.token) {
        this.getInfo();
      } else {
        console.error('JWT token not found in session storage');
      }
    },
    computed: {
      // Calculate total price based on quantity and unit price
      totalAmount() {
        return this.quantity * this.productData.unit_price;
      }
    },
    watch: {
      // Watch for changes in quantity or unit price to update total
      totalAmount() {
        this.productData.total = this.totalAmount;
      },
      'productData.unit_price'() {
        this.productData.total = this.totalAmount;
      }
    },
    methods: {

      async fetchData() {
      try {
        const response = await axios.get('getReview');
        this.products = response.data;
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
      toggleReviews() {
      this.showReviews = !this.showReviews;
    },
      opendialog(){
        this.dialogss = true;
      },
      closemodal(){
        this.dialogss = false;
      },

      async placeOrder(status) {
        try {
          const ins = await axios.post("placeOrder", {
            image: this.productData.image,
            prod_name: this.productData.prod_name,
            unit_price: this.productData.unit_price,
            size_id: this.productData.size_id,
            category_id: this.productData.category_id,
            quantity: this.quantity,
            address: this.info[0].address, // Assuming you want the first user's address
            contact: this.info[0].contact, // Assuming you want the first user's contact
            other_info: this.info[0].other_info, // Assuming you want the first user's other info
            token: this.info[0].token, // Assuming you want the first user's other info
            customerName: this.info[0].username,
            id: this.productData.id,
            transaction_code: this.productData.transaction_code,
            total: this.productData.total,
            status: status,
            
          });

          // Resetting data after order placement
          this.quantity = 1;
          this.customerName = "";

          // Triggering data retrieval after order placement
          await this.getInfo();

          if (status === 'cart') {
        // Open dialog for 'cart' status
        this.dialogs = true;
      } else if (status === 'pending') {
      this.dialog = true;
      }
        } catch (error) {
          console.error(error);
        }
      },
      async getInfo() {
        try {
          const response = await axios.get(`getUserData/${this.token}`);
          this.info = response.data;
        } catch (error) {
          console.error(error);
        }
      },
      getProductDetails() {
        this.productData.image = this.$route.params.image || '';
        this.productData.prod_name = this.$route.params.prod_name || '';
        this.productData.unit_price = this.$route.params.unit_price || 0;
        this.productData.size_id = this.$route.params.size_id || '';
        this.productData.stock = this.$route.params.stock || 0;
        this.productData.id = this.$route.params.id || '';
        this.productData.transaction_code = this.$route.params.transaction_code || '';
        this.productData.category_id = this.$route.params.category_id || '';
        
      },
      increaseQuantity() {
    if (this.quantity < this.productData.stock) {
      this.quantity += 1;
    } else {
      console.log('Maximum stock reached');
    }
  },
      decreaseQuantity() {
        if (this.quantity > 1) {
          this.quantity -= 1;
        }
      },
      async fetchSizes() {
        try {
          const response = await axios.get("getsize");
          this.productData.sizes = response.data;
        } catch (error) {
          console.error(error);
        }
      },
      getSizeName(sizeId) {
    const size = this.productData.sizes.find(size => size.size_id === sizeId);
    return size ? size.item_size : 'Unknown';
  },
    },
    mounted() {
      this.fetchSizes();
      this.getInfo();
      this.fetchData();
    },
  };
  </script>

  <style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Wallpoet&display=swap');

  @import url('https://fonts.googleapis.com/css2?family=Sacramento&display=swap');

  .neumorphic-navbar {
    scrollbar-width: thin;
    scrollbar-color: #b0b0b0 #f0f0f0;
  }
  
  .neumorphic-navbar::-webkit-scrollbar {
    width: 12px;
  }
  
  .neumorphic-navbar::-webkit-scrollbar-thumb {
    background-color: #b0b0b0;
    border-radius: 10px;
  }
  
  .neumorphic-circle {
    position: fixed;
    top: 20px;
    right: 20px;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background-color: #f0f0f0;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1), -2px -2px 5px rgba(255, 255, 255, 0.7);
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
  }
  
  .custom-icon {
    font-size: 16px;
  }

  @import url('https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css');
  @import url('https://fonts.googleapis.com/css2?family=Podkova&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Rochester&display=swap');
  /* Add additional styles if needed */
  .user-profile {
    width: 220px;
    margin-right: 100px;
  }
 
  </style>
