<template>
    <div>
        <div class="main">
        <button class="signup-button" @click="toggleLogin">Sign Up</button>
      </div>
    <div class="hero">
    <div class="hero-left">
    </div>
<div class="parent-container">
    
    <div class="progress-bar">
        
    </div>
    <div class="parent-heading">
        Satyam vada |  dharmam chara
    </div>
<div class="parent">
    <input type="text" class = "fname" placeholder = "First name" v-model="firstname">
    <input type="text" class = "lname" placeholder = "Last name" v-model="lastname">

    <input type="email" class = "email" placeholder = "Email" v-model="email" @blur="validateEmail">
    <span v-if="!isEmailValid" class="alert-message" style="color: red; font-size: 10px;">
          Invalid email 
    </span>
    
    <div class="dob-select-grp">
        <date-picker v-model="dob" valueType="format" class = "dob" placeholder = "DOB"></date-picker>
    <div class="select-grp" style = "height:1vh;display:flex; flex-direction:column;">
        <img :src="require(`~/components/gender.png`)" class = "select-img">
        <div class="select-grp--rad">
            <input type="radio" name="select" id="" v-model="gender">
            <input type="radio" name="select" id="" v-model="gender">
        </div>
    </div>
</div>
    <!-- <div class="div5"> </div> -->
    <select  class = "count" v-model="country"
                  :items="countries"
                  @click="getCountryInfo" >
                  <option
                    v-for="country in countries"
                    :key="country.id"
                    :value="country.name"
                  >
                    {{ country.name }}
                  </option>
    </select>

    <div class="phone-grp">
        <div class="country-flag">
            <img :src="getFlag(country)" />
        </div>
        <input type="text" class = "phone" placeholder = "getPhoneCode(country)"  v-model="phone" >
    </div>

        <div class="source-grp">
            <div class="search-icon">
            🔍
            </div>
            <div class="source-grp-1">Social media <input style = "width:1vw; height:4vh; background:none;" type = "radio" name = "source"></div>
            <div class="source-grp-2">Reference <input style = "width:1vw; height:4vh; background:none; " type = "radio" name = "source"></div>
            <div class="source-grp-3">News <input style = "width:1vw; height:4vh; background:none; " type = "radio" name = "source"></div>
        </div>
           <select class = "language" v-model="language" placeholder="Languages">
            <option value="" disabled>selected Languages</option>
                    <option value="English">English</option>
                    <option value="Malayalam">Malayalam</option>
                    <option value="Tamil">Tamil</option>
                    <option value="Teluhu">Teluhu</option>
                    <option value="Kannada">Kannada</option>
                    <option value="Hindi">Hindi</option></select>
           <input type="text" class = "special_remarks" placeholder = "Special remarks">
           <button class = "submit" type="submit" @click="openpopup"></button>

    
    </div>
</div>
    <div class="footer">
        <div class="footer-sub-grp"><span class = "footer-update">39997</span>
        <span class ="footer-head">Total meditators</span></div>
        <div class="footer-sub-grp"><span class = "footer-update">
            1136
        </span>
        <span class ="footer-head">Working numbers</span>
    </div>
        <div class="footer-sub-grp"><span class = "footer-update">39850</span><span class ="footer-head">Benefactories</span></div>
        <div class="footer-sub-grp">
            <span class = "footer-update">1648</span>
            <span class ="footer-head">Classes</span>
        </div>
    </div>
    
    <div class="pop hide">
<div class="pop-head">
    Confirm Email  & Phone Number ?
</div>
<div class="pop-content">
   

<span class="message"> +91 9072156487 & jasmin@gmail.com</span>
<span class="prompt">
Is this OK , or Would you like to edit  the Email & PhoneNumber ? 
</span> 
<div class="pop-btn">
    <button class="ok">OK</button>

    <button class="edit">Edit</button>
</div>
</div>

</div>
<div class="otp hide">
    <div class="otp-head">
        Enter otp
    </div>
    
    <div class="otp-content">
        <div class="otp-input-grp">
            
            
            <input id = 'otp-input' type="text">
            <input id = 'otp-input' type="text">
            <input id = 'otp-input' type="text">
            <input id = 'otp-input' type="text">
        </div>
        <div class="otp-timer">
1:30
        </div>

        <div class="otp-btn-grp">
            <button class="otp-submit">Submit</button><button class="resend">Resend </button>
        </div>
    </div>
</div>
</div>
</div>
</template>

<script>
import axios from "axios";
import DatePicker from 'vue2-datepicker';
import 'vue2-datepicker/index.css';
export default{
    components: {
        DatePicker,
    },
    data(){
        return{
            showpopup:false,
            firstname:"",
            lastname:"",
            email:"",
            isEmailValid: true,
            dob:"",
            gender:"",
            country:"",
            countries:[],
            flag:[],
            digitalcode:[],
            phone:[],
            referencecategory: "",
            language: [],
        }
    },
//     async mounted() {
//     await this.getCountryInfo();
//     // Set default values
//     this.country = this.selectedCountry;
//     this.phone = this.getPhoneCode(this.selectedCountry) ;
//   },
    methods:{
    async getCountryInfo() {
      try {
    const response = await axios.get(
      "http://89.47.164.122:4000/api/registrations/countrieslist"
    );
    const countryData = response.data;
    this.countries = countryData;
    this.flags = countryData.map((country) => country.flag);
    this.digitalCodes = countryData.map((country) => country.phonecode);

    // Find the index of the default country, for example, 'India'
    const defaultCountryIndex = this.countries.findIndex(
      (country) => country.name === 'India'
    );

    // Set the default values for the initial state
    this.selectedCountry = this.countries[defaultCountryIndex].name;
    this.selectedFlag = this.flags[defaultCountryIndex];
    this.selectedPhoneCode = this.digitalCodes[defaultCountryIndex];

      } catch (error) {
        console.error("Error fetching country information", error);
        throw error;
      }
    },
    getFlag(selectedCountry) {
      const index = this.countries.findIndex(
        (country) => country.name === selectedCountry
      );
      if (index !== -1 && this.flags && this.flags.length > index) {
        return this.flags[index];
      }
      return "";
    },

    getPhoneCode(selectedCountry) {
      const index = this.countries.findIndex(
        (country) => country.name === selectedCountry
      );
      if (
        index !== -1 &&
        this.digitalCodes &&
        this.digitalCodes.length > index
      ) {
        return this.digitalCodes[index];
      }
      return "";
    },
    async validateEmail() {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!emailRegex.test(this.email)) {
        this.isEmailValid = false;
      } else {
        this.isEmailValid = true;
       
      }
    },
    openPopup() {
        if (this.validateForm()) {
        this.showDialog = true;
        this.requestotp(); // Show the dialog box if the form is valid
      }
    },
    validateForm() {
      if (
        this.firstname === "" ||
        this.lastname === "" ||
        this.email === "" ||
        this.dob === "" ||
        this.country === "" ||
        this.phone === "" ||
        this.referencecategory === "" ||
        this.language === "" ||
        this.comments === ""
      ) {
        alert("Please fill in all fields");
        return false;
      }
      return true;
    },
    async requestotp() {
      const formdata = {
        first_name: this.firstname,
        last_name: this.lastname,
        DOB: this.dob,
        email: this.email,
        country: this.country,
        phone: this.phone,
        reference: this.referencecategory,
        language: this.language,
        remark: this.comments,
      };

      try {
        
        const response = await axios.post(
          "http://89.47.164.122:4000/api/registrations/registerUser",
          {
            phone: this.phone,
            formdata,
          }
        );
        console.log(response.data);
        if (response.status === 200) {
          console.log("OTP sent successfully:", response.data); 
        } 
      } catch (error) {
        if (error.response.status === 409) {
          alert("Email or phone number already exists. Please use a different email or phone number.");
        } else {
          console.error("Error requesting OTP:", error);
        }
      }
    },
    async resendotp() {
      try {
        const response = await axios.post("http://89.47.164.122:4000/api/registrations/resendOtp", {
          phone: this.phone, // Provide the phone number associated with the OTP
        });

        if (response.status === 200) {
          console.log("OTP resent successfully:", response.data);
          // Optionally, you can provide feedback to the user here
        }
      } catch (error) {
        console.error("Error resending OTP:", error);
        // Optionally, you can handle the error and provide feedback to the user
      }
    },
    async submitotp() {
  let OTP = this.otp;
  try {
    const response = await axios.post(
      "http://89.47.164.122:4000/api/registrations/verify_otp",
      {
        OTP: OTP,
        phone: this.phone,
      }
    );
    if (response.status === 200) {
      console.log(response, 'submit');
      alert("Registration Successful");
      // if (response.data.toLowerCase() === 'submit') {
        
      // }
      //  else {
      //   alert("Invalid OTP. Please try again.");
      // }
    }
  } catch (error) {
    console.error("Error while submitting OTP:", error);
    alert("Entered a wrong OTP");
}
    }
}
}
</script>


<style>
* {
  margin: 0;

  font-family: "Poppins", sans-serif;
}
.alert-message {
    color: red;
    font-size: 12px;
    display: block;
    left: 5px;
   /* Adjust margin as per your design */
  }
.hero {
  display: flex;
}
.hero-left {
  background-image: url("../components/step.jpg");
  background-repeat: no-repeat;

  background-size: auto 100%;
  width: 38vw;
  height: 100vh;
}
.parent-heading {
color:#05616d;
  font-size: 1.6rem;
  position: absolute;
  top: 4vh;
}

.footer {
  width: 60vw;

  display: flex;
  /* flex-direction: column; */
  justify-content: space-between;
  position: absolute;
  bottom: 3vh;
  left: 35vw;
}
.footer .footer-sub-grp {
  display: flex;

  flex-direction: column;
  align-items: center;
}
.footer .footer-sub-grp .foot-head {
  font-weight: 500;
}
.footer .footer-sub-grp .footer-update {
  font-weight: bold;
}
.blur {
  filter: blur(4px);
  -webkit-filter: blur(4px);
}
.hide {
  display: none !important;
}
.pop {
    display:flex;
    
    flex-direction: column;
    box-shadow: 1px 7px 10px 9px rgba(0,0,0,0.26);
  width: 30vw;
  height: 17vw;
  background-color: rgb(255, 255, 255);
  position: absolute;
  top: 35vh;

  left: 45vw;
  z-index: 100;
  border-radius: 17px;
}
.pop-head{
    width:100%;
    height:9vh;
   
    background-color: rgba(219, 98, 98, 1);
  border-top-left-radius: 17px;
  border-top-right-radius: 17px;
  color:white;

  font-weight:600;
  display: flex;
  
  justify-content: center;

  
  
  align-items: center;
}

.pop-content{
    height: 21vh;
    display: flex;
    flex-direction: column;
    align-items: space-between;
    align-items: center;
    justify-content: space-between;
   
}


.pop-content .message{
    margin-top:2vh;
    font-size:1rem;
    color:rgb(211, 58, 58);
}
.pop-content .prompt{
    font-size:0.8rem; 
}
.pop-content .pop-btn{
    width:100%;
    display: flex;
    justify-content:space-around;
}
.pop-content .ok,.edit{
    width:7vw;
    height:5vh;
    border-radius:7px;
    border:none;
}
.pop-content .ok{
    box-shadow: 1px 7px 10px 9px rgba(0,0,0,0.26);
 
    background-color: #fff;
    color:black;
}
.pop-content .edit{
    box-shadow: 1px 7px 10px 9px rgba(0,0,0,0.26);

    background-color: black;
    color:white;
}

.otp{
    display:flex;
    
    flex-direction: column;
    box-shadow: 1px 7px 10px 9px rgba(0,0,0,0.26);
  width: 30vw;
  height: 17vw;
  background-color: rgb(255, 255, 255);
  position: absolute;
  top: 35vh;

  left: 45vw;
  z-index: 100;
  border-radius: 17px;
}

.otp-head{
    width:30vw;
    height:7vh;
    background-color:rgba(61, 129, 132, 1);
    border-top-left-radius: 17px;
    border-top-right-radius: 17px;
    
    color:white;
    font-weight: bold;
    display: flex;
    justify-content:center;
    align-items:center;
}
.otp-content{
    height:10vh;        
    width:30vw;
    
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    position: relative;
    top:2vh;
}
.otp-timer{
    font-size:1.6rem;
    position: relative;
    top:3vh;
}
.otp-btn-grp{
    position: relative;
    top:3vh;
    width:30vw;
    display:flex;
    
    justify-content: space-around;
}
.otp-content .otp-input-grp #otp-input{
    
    width:4vw;
    height:8vh;
    border:1px solid black;
}





.otp-btn-grp .otp-submit{
   
     
        width:7vw;
        height:5vh;
        border-radius:7px;
        border:none;
}
.otp-btn-grp .resend{
   
 
    width:7vw;
    height:5vh;
    border-radius:7px;
    border:none;
    background-color: rgba(61, 129, 132, 1);
    color:white;
}
.parent-container {
  height: 100vh;

  width: 100%;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-image: url("../components/bg.jpeg");
  background-repeat: no-repeat;
  background-size: 100% auto;
  background-position-x: 50%;
  background-position-y: -14vh;
}

.progress-bar{
    width:72.5vw;
    height:2vh;
    background-color: rgba(7, 98, 109, 1);
    position: absolute;
    top:0;
    z-index:1500;
    transition: all 0.5s ease-in-out;
}
.progress-bar:hover{
    width:72.5vw;
    height:7vh;
    background-color: rgba(7, 98, 109, 1);
    position: absolute;
    top:0;
    z-index:1500;
}
.parent {
  height: 60vh;
  width: 60vw;
  display: grid;
  grid-template-columns: repeat(2, 2fr);
  grid-template-rows: repeat(6, 1fr);
  grid-column-gap: 1.6rem;
  grid-row-gap: 1.6rem;
}

.fname {
  grid-area: 1 / 1 / 2 / 2;
}
.lname {
  grid-area: 1 / 2 / 2 / 3;
}
.email {
  grid-area: 2 / 1 / 3 / 2;
}

.dob-select-grp {
  grid-area: 2 / 2 / 10 / 3;
  display: flex;
  justify-content: space-between;
}
.dob{
    width:23vw;
}
.count {
  grid-area: 3 / 1 / 4 / 2;
}
.phone-grp {
  grid-area: 3 / 2 / 4 / 3;
  display: grid;
  grid-template-columns: 1fr 4fr;
  grid-gap: 1.1rem;
}
.grp {
  grid-area: 4 / 1 / 5 / 2;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
.source-grp{
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #fff;
}
.language {
  grid-area: 4 / 2 / 5 / 3;
}

.special_remarks {
  grid-area: 5 / 1 / span 1 / span 2;
}
.submit {
  background-color: rgba(0, 0, 0, 0.7);
  color: white;
  border: none;
  grid-area: 6 / 1 / span 1 / span 2;
}


.select-img{
    height: 7vh;
    position: relative;
    top: -1vw;
}
::placeholder {
  color: #05616d;
  font-size: 1rem;
}
input[type=text],.submit,
.country-flag,
.source-grp,
select {
  height: 7vh;
  border: none;
  border: 0.7px solid white;
  box-shadow: 1px 7px 10px 2px rgba(0, 0, 0, 0.26);
  outline: none;
  border-radius: 4px;
  font-size: 1rem;

  color: #05616d;
  box-sizing: border-box;
  padding-left: 11px;
}
.select-grp {
  position: relative;
}

.source-grp {
  display: flex;
}

.source-grp-1,
.source-grp-2,
.source-grp-3 {
  /* /* box-sizing: border-box; */
  display: grid;
  grid-auto-rows: minmax(100px auto);
  grid-auto-columns: minmax(100px auto);

  /* grid-column-gap:20px; */
}
.select-grp--rad {
  width: 90%;
  display: flex;

  justify-content: space-between;
  position: absolute;
  top: 5vh;

  right: 0;
}
.submit{
    color:white;
    border:none;
}
/* media query */
@media (max-width:1200px){
    .hero-left{
        width:34vw;
    }
}

@media (max-width:1024px){
    .parent-heading {
        color:#05616d;
          font-size: 1.4rem;
          /* position: absolute;
          top: 4vh; */
        }
        .hero-left{
            width:42vw;
        }
}

@media (max-width:768px){
    .parent-heading {
        color:#05616d;
          font-size: 1.4rem;
          position: absolute;
          top: 4vh;
        }
        .hero-left{
            width:42vw;
        }
        .parent {
            /* height: 60vh; */
            width: 40vw;
           
          }
        }

        @media (max-width:568px){
            .hero {
                display: flex;
                flex-direction: column;
              }
              .parent-container{
                position: absolute;
                top:55vh;
              }
            .parent-heading {
                color:#05616d;
                  font-size: 1rem;
                  position: relative;
                  top: -5vh;
                }
                .hero-left{
                    width:42vw;
                }
                .parent {
                    /* height: 60vh; */
                    width: 95vw;
                   
                  }
                  .hero-left {
                    background-image: url("../components/step.jpg");
                    background-repeat: no-repeat;
                  
                    background-size: 100% auto;
                    width: 100vw;
                    /* height: 100vh;  */
                  

                  }
                    
                  .dob{
                    width:32vw;
                  }
                  .footer {
                    width: 90vw;
                  
                    display: flex;
                    /* flex-direction: column; */
                    justify-content: space-between;
                    position: relative;
                    top:10vh;
                   
                  }
                  .footer .footer-sub-grp .footer-update {
                    font-size:0.7rem;
                  }
                  .footer .footer-sub-grp .footer-head {
                    font-size:0.7rem;
                  }
                }  
                
                </style>
