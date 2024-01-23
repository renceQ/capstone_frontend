<template>
	
	<form @data-saved="getUserDetails" />
	<div>
		<tr v-for="info in info">
			<td>{{ info.category_name}}</td>
			<td>
			  <button @click="editprofile" class="btn btn-success btn-sm edit">Edit profile</button>
			</td>
		  </tr>
	</div>
	<br>
	<br>
	<br>
	<br>
	<br>
    <div style="display: flex; align-items: center;">
		<img :src="require('../../../public/img/black2.png')" alt="Description of the image" style="width: 400px; margin-left: 170px; margin-right: 0px; margin-top: 30px; transition: transform 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);">

		<div style="margin-left:10px;">
			<br>
			<br>
			<br>
			<br>
	
			<h1 class="text-center" style="font-size: 20px;font-size:20px; font-weight:900;  margin-right:255px; margin-top:10px;">WELCOME TO QMJ <span style="font-size: 32px;  font-weight:100;">|</span>&nbsp;&nbsp; <span style="position:absolute;top:180px;font-size:73px; font-weight:400; font-family: 'WindSong', cursive;">Images...</span></h1>
		
			<h2 class="navbar-brand" href="index.html" style="margin-top:40px;font-size: 16px;">
				Youre one stop destination for memorable experiences!
				<br>Explore our curated book event services, discover<br>
				  unique products, and personalized items to make each<br>
			moment uniquely yours, Immerse yourself in a world<br>
			of creativity and possibilities. Let's create unforgettable <br>
			memories together!.
			</h2>
			<div>
				<br>
				<br>
				<router-link
  to="/about"
  class="neumorphic-link"
  style="
	
    padding: 10px 20px;
    font-size: 16px;
    background: linear-gradient(45deg, #000, #6d6d6d);
    border: none;
	color:white;
    border-radius: 4px;
    box-shadow: 4px 4px 8px #c7c7c7, -4px -4px 8px #ffffff;
    transition: all 0.3s ease;
    text-decoration: none; /* Remove underline */
    display: inline-block; /* To remove underline */
    position: relative; /* For pseudo-element */
  "
>
  Explore
</router-link>

<span>	
	
	
	<router-link
	to="/userServices"
	class="neumorphic-link"
	style="
	  margin-left:8px;
	  padding: 10px 20px;
	  font-size: 16px;
	  background-color: rgb(151, 150, 150);
	  height:45px;
	  color:white;
	  border-radius: 4px;
	  box-shadow: 4px 4px 8px #c7c7c7, -4px -4px 8px #ffffff;
	  transition: all 0.3s ease;
	  text-decoration: 1pxx; /* Remove underline */
	  display: inline-block; /* To remove underline */
	  position: absolute; /* For pseudo-element */
	  height:43.5px;
	"
  >
	Our Services
  </router-link></span>

			</div>
			<br>
		
		</div>
	</div>
</template>

<style scoped>
img:hover {
    transform: scale(1.1);
   
  }
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
.neumorphic-link {
	/* Your existing styles */
	/* ... */
  
	/* Remove underline by default */
	text-decoration: none;
  }
  
  .neumorphic-link:hover {
	/* Style on hover */
	background-color: #ddd;
	box-shadow: 5px 5px 10px #bcbcbc, -5px -5px 10px #ffffff;
	color: #000000; /* Change text color on hover */
  }
  
  /* Hide the underline only on hover */
  .neumorphic-link::after {
	content: '';
	position: absolute;
	left: 0;
	right: 0;
	bottom: -5px; /* Adjust this value to fine-tune the positioning */
	height: 1px;
	background-color: transparent; /* Make the underline transparent */
	transition: all 0.3s ease;
  }
  
  .neumorphic-link:hover::after {
	bottom: -10px; /* Move the underline away on hover */
	background-color: transparent; /* Hide the underline on hover */
  }
</style>

<script>


</script>