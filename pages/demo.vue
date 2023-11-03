<template>
    <div>
      <div class="main">
       
        <select class = "homelang" v-model="hlanguage" name="Languages" placeholder="Languages">
            <option value="languages"  >selected Languages</option>
                    <option value="English">English</option>
                    <option value="Malayalam">Malayalam</option>
                    <option value="Tamil">Tamil</option>
                    <option value="Telugu">Telugu</option>
                    <option value="Kannada">Kannada</option>
                    <option value="Hindi">Hindi</option></select> 
        <button class="signup-button" @click="toggleLogin">Proceed</button>
      </div>
  
      <div :class="{ 'login-container': true, 'show-login': isLoginVisible }">
        <!-- Your registration form and content -->
        <!-- ... Your existing HTML content ... -->


        <div class="hero">
        
    <div class="parent-container">
        
        <div class="progress-bar">
          <div class="audio-player">
  <div class="timeline">
    <div class="progress"></div>
  </div>
  <div class="controls">
    <div class="play-container">
      <div class="toggle-play play">
    </div>
    </div>
    <div class="time">
      <div class="current">0:00</div>
      <div class="divider">/</div>
      <div class="length"></div>
    </div>
    <div class="name">English </div>
<!--     credit for icon to https://saeedalipoor.github.io/icono/ -->
    <div class="volume-container">
      <div class="volume-button">
        <div class="volume icono-volumeMedium"></div>
      </div>
      
      <div class="volume-slider">
        <div class="volume-percentage"></div>
      </div>
    </div>
  </div>
</div>
        </div>
        <div class="parent-heading">
            Satyam vada |  dharmam chara
        </div>
    <div class="parent">
        <input type="text" class = "fname" placeholder = "First name" v-model="firstname">
        <input type="text" class = "lname" placeholder = "Last name" v-model="lastname">
    
        <input type="email" class = "email" placeholder = "Email" v-model="email">
        <div class="dob-select-grp">
            <date-picker v-model="dob" valueType="format" class = "dob" placeholder = "DOB"></date-picker>
        <div class="select-grp" style = "height:1vh;display:flex; flex-direction:column; left: 23.5vw;">
            <img src = "../components/gender.png" class = "select-img">
            <div class="select-grp--rad">
                <input type="radio" name="select" id=""  v-model="gender" value="Female">
                <input type="radio" name="select" id=""  v-model="gender" value="Male">
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
          <div class="country-flag" style="background-color: white;">
                <img
                    :src="getFlag(country)"
                    class="country-flag-img"
                />
            </div>


            <div class="phone-number-container">
              <span style="font-size: 20px;">{{getPhoneCode(country)}}</span>
              <input
                  class="phoneNumber"
                  placeholder="Ph No"
                  type="phone"
                  v-model="phone"

            />
            </div>
                
    
        </div>
            <div class="source-grp" style="background-color: white;">
                <div class="search-icon">
                🔍
                </div>
                <div class="source-grp-1" >Social media <input v-model="referencecategory" 
                value="socialmedia"
                 style = " width:1vw; height:4vh; display: flex;
                position: relative; 
                left: 2vw;  background:none;" type = "radio" name = "source"></div>
                <div class="source-grp-2">Reference <input v-model="referencecategory" value="reference" style = " width:1vw; height:4vh;  display: flex;
                position: relative;
                 left: 2vw;
                 background:none;" type = "radio" name = "source"></div>
                <div class="source-grp-3">Others <input v-model="referencecategory" value="others" style = "width:1vw; height:4vh;  display: flex;
                position: relative; left: 1vw;background:none;" type = "radio" name = "source"></div>
            </div>
            
    
    
      
            <select class = "language" v-model="language">
            <option value="" selected>selected Languages</option>
                    <option value="English">English</option>
                    <option value="Malayalam">Malayalam</option>
                    <option value="Tamil">Tamil</option>
                    <option value="Teluhu">Teluhu</option>
                    <option value="Kannada">Kannada</option>
                    <option value="Hindi">Hindi</option></select>
    
               <input type="text" class = "special_remarks" placeholder = "Special remarks" v-model="comments">
            
               <button class = "submit" type="submit" value ="Submit" @click="handleFormSubmit">Submit</button>
    
        
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
        
    </div>
    <div v-if="showPopup" class="pop1">
    <div class="head1">
        Confirm Email  & Phone Number ?
    </div>
    <div class="popcontent">
       
    
    <span class="message1">{{email}} & {{ phone }}</span>
    <span class="prompt">
    Is this OK , or Would you like to edit  the Email & PhoneNumber ? 
    </span> 
    <div class="popbtn">
        <button class="ok" @click="getotp">OK</button>
    
        <button class="edit" @click="closepopup">Edit</button>
    </div>
    </div>
    
    </div>

    <div v-if="showPopup1" class="pop1">
    <div class="head1">
        
    </div>
    <div class="popcontent">
       
    Registration Sucessful
   
    <div class="popbtn">
    <button class="ok">OK</button>
    
        
    </div>
    </div>
    
    </div>
    <!-- <div v-if="showPopup" class="pop hide">
    <div class="pop-head">
        Confirm Email  & Phone Number ?
    </div>
    <div class="pop-content">
       
    
    <span class="message">{{ enteredData }}</span>
    <span class="prompt">
    Is this OK , or Would you like to edit  the Email & PhoneNumber ? 
    </span> 
    <div class="pop-btn">
        <button class="ok">OK</button>
    
        <button class="edit">Edit</button>
    </div>
    </div>
    
    </div> -->
    
    <div  v-if="openpopup && !showPopup" class="otp1">
        <div class="otphead">
            Enter otp
        </div>
        <div class="otpcontent">
            <div class="otpinputgrp">
                
              <input
      v-model="otpInput1"
      type="text"
      maxlength="1"
      @input="focusNext(1)"
      style="width: 2em; text-align: center; margin: 0 0.2em;"
    />
    <input
    v-model="otpInput2"
      type="text"
      maxlength="1"
      @input="focusNext(2)"
      style="width: 2em; text-align: center; margin: 0 0.2em;"
    />
    <input
    v-model="otpInput3"
      type="text"
      maxlength="1"
      @input="focusNext(3)"
      style="width: 2em; text-align: center; margin: 0 0.2em;"
    />
    <input
    v-model="otpInput4"
      type="text"
      maxlength="1"
      style="width: 2em; text-align: center; margin: 0 0.2em;"
    />
            </div>
            <div class="otptimer">
    1:30
            </div>
    
            <div class="otpbtngrp">
                <button class="otpsubmit" @click="submitotp">Submit</button>
                <button class="resend" @click="resendotp">Resend </button>
            </div>
        </div>
    </div>
    

    <div v-if="showRegistrationForm " class="overlay">
      <div class="registration-card">
        
        <div class="card-div-top">
          <div class="card-number">
              <p>card number</p>
              <h1>10040</h1>
          </div>
          <div class="card-logo-container">
              <img class="card-logo" src="../components/logo.png" alt="Thasmai logo"/>
          </div>
        </div>

        <div class="card-div-middle">
          <img class="chip" src="../components/chip.png" alt="chip">
          <h3>Registration Successful</h3>
          <button>OK</button>
        </div>

        <div class="card-div-bottom">
          <div class="cardholder-group">

            <div class="cardholder-name">
              <p>Cardholder Name</p>
              <h2>{{ this.firstname }}{{ this.lastname }}</h2>
            </div>
            <div class="cardholder-img-container">
              <img class="cardholder-img" src="../components/user.png" alt="User logo"/>
            </div>

          </div>

          <div class="validity">
            <p>VALID THRU</p>
            <p>11/27</p>
          </div>
        </div>



      </div>
    </div>
        <!-- <div class="otp-content">
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
    </div> -->
    </div>
    
      </div>
  
      <div class="a">
        <div :class="{ 'image-background': isRedBackground }"></div>
      </div>
  
      <!-- Pop-up dialog -->
      <div class="popup-container" v-if="popupVisible">
        <!-- ... Pop-up content ... -->
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
          showRegistrationForm: false,
            isRedBackground: false,
            showPopup: false,
            openpopup:false,
            showPopup1:false,
            hlanguage:'',
            enteredData: '',
            firstname:'',
            lastname:'',
            email:'',
            isEmailValid: true,
            dob:'',
            gender:'',
            country:'',
            countries:[],
            flag:[],
            digitalcodes:[],
            phone:[],
            referencecategory: '',
            language: [],
            comments:'',
            popupVisible:false,
            otpInput1:'',
            otpInput2:'',
            otpInput3:'',
            otpInput4:'',
            otp:'',
            audiosource:{
              English:'/audio/TSL_ENGLISH.mp4',
              Malayalam : '/audio/TSL_Malayalam.mp4',
              Hindi : '/audio/TSL_Hindi.mp4',
              Tamil : '/audio/TSL_Tamil.mp4',
              Kannada : '/audio/TSL_Kannada.mp4',
              Telugu:'/audio/TSL_Telugu.mp4'
            },
            audio:null
        }
    },
    // mounted() {
    //   let sub = document.querySelector(".submit")
    // let editbtn = document.querySelector(".edit")
   
    // let otp = document.querySelector(".otp")
    // let okbtn = document.querySelector(".ok")

    
    
    
    // let div = document.querySelector('.parent-container')


    // },
    async mounted() {
    await this.getCountryInfo();
    // Set default values
    this.country = this.selectedCountry;
    this.phone = this.getPhoneCode(this.phonecode) ;


    const audioElement = this.$refs.audioElement;
    this.audio = new Audio(this.audiosource[this.languagehome]);
    // const audioPlayer = document.querySelector(".audio-player");

 const lang = document.querySelector(".homelang")
 const audiosource = {
              English:'/audio/TSL_ENGLISH.mp4',
              Malayalam : '/audio/TSL_Malayalam.mp4',
              Hindi : '/audio/TSL_Hindi.mp4',
              Tamil : '/audio/TSL_Tamil.mp4',
              Kannada : '/audio/TSL_Kannada.mp4',
              Telugu:'/audio/TSL_Telugu.mp4'
            }
 let audio = new Audio("/audio/TSL_ENGLISH.mp4")
 console.log(lang.value || "q",'qwerty')
 const language = lang.value || 'English';

const audiopath = `${audiosource[`${language}`]}`
 lang.addEventListener("change",()=>{
  
  
 
  console.log(language,lang.value) 
  audio = new Audio(
   `${audiopath}`
);

const audioPlayer = document.querySelector(".audio-player");

//credit for song: Adrian kreativaweb@gmail.com

console.log(audio,"plort");

audio.addEventListener(
  "loadeddata",
  () => {
    audioPlayer.querySelector(".time .length").textContent = getTimeCodeFromNum(
      audio.duration
    );
    audio.volume = .75;
  },
  false
);

//click on timeline to skip around
const timeline = audioPlayer.querySelector(".timeline");
timeline.addEventListener("click", e => {
  const timelineWidth = window.getComputedStyle(timeline).width;
  const timeToSeek = e.offsetX / parseInt(timelineWidth) * audio.duration;
  audio.currentTime = timeToSeek;
}, false);

//click volume slider to change volume
const volumeSlider = audioPlayer.querySelector(".controls .volume-slider");
volumeSlider.addEventListener('click', e => {
  const sliderWidth = window.getComputedStyle(volumeSlider).width;
  const newVolume = e.offsetX / parseInt(sliderWidth);
  audio.volume = newVolume;
  audioPlayer.querySelector(".controls .volume-percentage").style.width = newVolume * 100 + '%';
}, false)

//check audio percentage and update time accordingly
setInterval(() => {
  const progressBar = audioPlayer.querySelector(".progress");
  progressBar.style.width = audio.currentTime / audio.duration * 100 + "%";
  audioPlayer.querySelector(".time .current").textContent = getTimeCodeFromNum(
    audio.currentTime
  );
}, 500);

//toggle between playing and pausing on button click
const playBtn = audioPlayer.querySelector(".controls .toggle-play");
playBtn.addEventListener(
  "click",
  () => {
    if (audio.paused) {
      playBtn.classList.remove("play");
      playBtn.classList.add("pause");
      audio.play();
    } else {
      playBtn.classList.remove("pause");
      playBtn.classList.add("play");
      audio.pause();
    }
  },
  false
);

audioPlayer.querySelector(".volume-button").addEventListener("click", () => {
  const volumeEl = audioPlayer.querySelector(".volume-container .volume");
  audio.muted = !audio.muted;
  if (audio.muted) {
    volumeEl.classList.remove("icono-volumeMedium");
    volumeEl.classList.add("icono-volumeMute");
  } else {
    volumeEl.classList.add("icono-volumeMedium");
    volumeEl.classList.remove("icono-volumeMute");
  }
});

//turn 128 seconds into 2:08
function getTimeCodeFromNum(num) {
  let seconds = parseInt(num);
  let minutes = parseInt(seconds / 60);
  seconds -= minutes * 60;
  const hours = parseInt(minutes / 60);
  minutes -= hours * 60;

  if (hours === 0) return `${minutes}:${String(seconds % 60).padStart(2, 0)}`;
  return `${String(hours).padStart(2, 0)}:${minutes}:${String(
    seconds % 60
  ).padStart(2, 0)}`;
}
})
  },
  computed: {
    formattedPhoneNumber: {
      get() {
        return `${this.getPhoneCode(this.country)} ${this.phone}`;
      },
      set(value) {
        const code = this.getPhoneCode(this.country);
        const phone = value.replace(code + "").trim(); // removing the code from the input value
        this.phone = phone;
        console.log(phone);
      },
    },
  },
    methods:{
        toggleLogin() {
        this.isLoginVisible = !this.isLoginVisible;
        this.isRedBackground = !this.isRedBackground;
      },
      async getCountryInfo() {
      try {
        const response = await axios.get("http://89.47.164.122:5000/api/registrations/countrieslist");
        const countryData = response.data;
        this.countries = countryData;
        this.flags = countryData.map((country) => country.flag);
        this.digitalcodes = countryData.map((country) => country.phonecode);
        this.digitalCodes = countryData.map((country) => country.phonecode);

        // console.log( this.digitalcodes);
       const defaultCountryIndex = this.countries.findIndex((country) => country.name === 'India');

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
      const index = this.countries.findIndex((country) => country.name === selectedCountry);
      if (index !== -1 && this.digitalCodes && this.digitalCodes.length > index) {
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
    validateForm() {
      if (
        this.firstname === "" ||
        this.lastname === "" ||
        this.email === "" ||
        this.dob === "" ||
        this.country === "" ||
        this.phone === "" ||
        this.referencecategory === "" ||
        this.language === "" 
      ) {
        
        alert("Please fill in all fields");
        return false;
      }
      return true;

    },

    handleFormSubmit() {
      if (this.validateForm()) {
        this.showPopup = true;

        console.log('sucess');
        // let sub = document.querySelector(".submit")
      }
    },
    closepopup(){
      this.showPopup = false;
    },
    focusNext(index) {
      if (index < 4) {
        this.$refs[`otpInput${index + 1}`][0].focus();
      }
    },
    getotp() {
      this.requestotp();
      this.showPopup = false;
      this.openpopup= true;

    },
    focusNext(index) {
      if (index < 4) {
        const nextInput = this.$refs[`otpInput${index + 1}`];
        const currentInput = this.$refs[`otpInput${index}`];
        
        if (currentInput && currentInput.value.length === 1) {
          nextInput.focus();
        }
      }
    },
    async requestotp() {
      
      try {
        
        axios.post(
          "http://89.47.164.122:5000/api/registrations/registerUser",
          {
            phone: this.phone,
            first_name: this.firstname,
            last_name: this.lastname,
            DOB: this.dob,
            gender: this.gender,
            email: this.email,
           country: this.country,
           phone: this.phone,
          reference: this.referencecategory,
          language: this.language,
           remark: this.comments,
             
          }
        ).then((res)=>{
          console.log(res)
        })
        .catch((err)=>{
          alert('user already exist')
        })
        console.log(response);
        if (response.status === 200) {
          console.log("OTP sent successfully:", response.data);
          this.showPopup1 = true;
          this.showRegistrationForm = false;
        } 
        else{
          alert('user already exist')
         
         
        }
      } catch (error) {
        console.error("Error requesting OTP:", error);
      }
    },
    // async requestotp() {
    //   // const formdata = {
    //   //   first_name: this.firstname,
    //   //   last_name: this.lastname,
    //   //   DOB: this.dob,
    //   //   email: this.email,
    //   //   country: this.country,
    //   //   phone: this.phone,
    //   //   reference: this.referencecategory,
    //   //   language: this.language,
    //   //   remark: this.comments,
    //   // };
    //   const formdata ={
    //     first_name:"abc",
    //     last_name: "hds",
    //     DOB: "12/02/2020",
    //     email: "dds@gmail.com",
    //     gender:"Male",
    //     country: "India",
    //     phone: "8281173501",
    //     reference: "others",
    //     language: "Malayalam",
    //     remark: "yhujij",
    //   }

    //   try {
        
    //     const response = await axios.post(
    //       "http://89.47.164.122:5000/api/registrations/registerUser",
    //      formdata
    //     );
    //     console.log(formdata)
    //     console.log(response.data);
    //     if (response.status === 200) {
    //       console.log("OTP sent successfully:", response.data); 
    //     } 
    //   } catch (error) {
    //     if (error.response.status === 409) {
    //       alert("Email or phone number already exists. Please use a different email or phone number.");
    //     } else {
    //       console.error("Error requesting OTP:", error);
    //     }
    //   }
    // },
    async resendotp() {
      try {
        const response = await axios.post("http://89.47.164.122:5000/api/registrations/resendOtp", {
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
    let  otp= this.otpInput1+this.otpInput2+this.otpInput3+this.otpInput4;
  try {
    const response = await axios.post(
      "http://89.47.164.122:5000/api/registrations/verify_otp",
      {
        OTP: otp,
        phone: this.phone,
      }
    );
    if (response.status === 200) {
      console.log(response, 'submit');
      this.showRegistrationForm = true;
      // alert("Registration Successful");
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
    },
    


}
}
</script>

<style>
* {
      margin: 0;
 
      font-family: "Poppins", sans-serif;
    }
    .hero {
      display: flex;
    }
    .hero-left {
      /* background-image: url("../components/side.jpeg"); */
      /* background-repeat: no-repeat; */
      background-color: transparent; 
 
      background-size: auto 100%;
      width: 38vw;
      height: 100vh;
    }
    .homelang{
      background-color: white;
    color: rgba(0, 0, 0, 0.7);
    border: none;
    width: 15vw;
    display: flex;
    position: absolute;
    top: 53vh;
    left: 83vw
    }
    .parent-heading {
    color:#05616d;
      font-size: 1.6rem;
      position: absolute;
      top: 7vh;
    }
 
    .footer {
      width: 60vw;
 
      display: flex;
      /* flex-direction: column; */
      justify-content: space-between;
      position: absolute;
      bottom: 3vh;
    }
    .footer .footer-sub-grp {
      display: flex;
 
      flex-direction: column;
      align-items: center;
    }
    .footer .footer-sub-grp .footer-head {
      font-weight: 600;
    }
    .footer .footer-sub-grp .footer-update {
      font-weight: bold;
      font-size: 1.3rem;
      /* color: white; */
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
      background-position-y: -12vh;
 
    }
 
 
    .progress-bar{
        width:100%;
        height:5vh;
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
    .phone-number-container{
      display: flex;
      position: relative;
      align-items: center;
    }
    .phoneNumber {
      position: absolute;
      right: 0;
      display: flex;
      left: 2vw;
 
    }
    .grp {
      grid-area: 4 / 1 / 5 / 2;
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
    }
    .source-grp{
        display: flex;
        justify-content: space-around;
        align-items: center;
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
    input[type=text],
     input[type=email], 
     input[type=phone],
     .submit,
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
 
    .country-flag-img {
      height: 5vh;
    position: relative;
    top: 0.8vh;
    display: flex;
    justify-content: center;
    align-items: center;
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
    .pop1{
      display: flex;
    width: 30vw;
    height: 39vh;
    position: absolute;
    top: 35vh;
    left: 16vw;
    background-color: #f0f3f3;
    border-radius: 7px;
    /* border-radius: 2; */
    }
    .head1{
      width: 100%;
      height: 7vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
    position: absolute;
    top: 0vh;
    background-color: #DB6262;
    color: #fff;
    border-top-left-radius: 7px;
    border-top-right-radius: 7px;
    }
    .popcontent{
      height: 21vh;
        display: flex;
        flex-direction: column;
        align-items: space-between;
        align-items: center;
        justify-content: space-between;
    }
 
    .popcontent .message1{
      width: 18vw;
    display: flex;
    position: relative;
    /* margin-top: 2vh; */
    top: 10vh;
   justify-content: center;
    font-size: 1rem;
    color:#DB6262
    }
    .popcontent .prompt{
      font-size: 0.8rem;
    position: relative;
    top: 11vh;
    display: flex;
    justify-content: center;
    left: 5vw;
    }
    .popcontent .popbtn{
      width: 100%;
    display: flex;
    justify-content: space-around;
    position: relative;
    top: 11vh;
 
    }
    .popcontent .ok,.edit{
        width:7vw;
        height:5vh;
        border-radius:7px;
        border:none;
    }
    .popcontent .ok{
        box-shadow: 1px 7px 10px 9px rgba(0,0,0,0.26);
 
        background-color: #fff;
        color:black;
    }
    .popcontent .edit{
        box-shadow: 1px 7px 10px 9px rgba(0,0,0,0.26);
 
        background-color: black;
        color:white;
    }
    .otpcontent{
      height:10vh;        
        width:30vw;
 
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;
        position: relative;
        top:2vh;
    }
    .otp1{
      width: 30vw;
      height: 41vh;
      display: flex;
    position: absolute;
    top: 35vh;
    left: 11vw;
    background-color: #e9eded;
    border-radius: 17px;
    }
    .otphead{
      width: 30vw;
    height: 7vh;
    position: absolute;
    background-color: rgba(61, 129, 132, 1);
    border-top-left-radius: 17px;
    border-top-right-radius: 17px;
    color: white;
    font-weight: bold;
    display: flex;
    justify-content: center;
    align-items: center;
    }
    .otpcontent{
      height: 10vh;
    width: 30vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    position: absolute;
    top: 16vh;
    }
    .otpinputgrp #otp-input{
      width:4vw;
        height:8vh;
        border:1px solid black;
    }
    .otptimer{
      font-size:1.6rem;
        position: relative;
        top:3vh;
    }
    .otpbtngrp{
      position: relative;
    top: 2vh;
    left: 0vw;
 
    width: 30vw;
    display: flex;
    justify-content: space-around;
}
 
 
   .otpbtngrp .otpsubmit{
            width:7vw;
            height:5vh;
            border-radius:7px;
            border:none;
    }
    .otpbtngrp .resend{
      width:7vw;
            height:5vh;
            border-radius:7px;
            border:none;
            background-color: rgba(61, 129, 132, 1) ;
    }
    .audio-player {
    /* Add your custom styles for the audio player container */
    height: 40px;
  width:100%;
  background-color: rgba(7, 98, 109, 1);
  box-shadow: 0 0 20px 0 #000a;
  font-family: arial;
  color: white;
  font-size: 0.75em;
  overflow: hidden;
  display: grid;
  grid-template-rows: 6px auto;
  }
  .audio-player .timeline {
  background: white;
  width: 100%;
  position: relative;
  cursor: pointer;
  box-shadow: 0 2px 10px 0 #0008;
}
.audio-player .timeline .progress {
  background: coral;
  width: 0%;
  height: 100%;
  transition: 0.25s;
}
.audio-player .controls {
  display: flex;
  justify-content: space-between;
  align-items: stretch;
  padding: 0 20px;
}
.audio-player .controls > * {
  display: flex;
  justify-content: center;
  align-items: center;
}
.audio-player .controls .toggle-play.play {
  cursor: pointer;
  position: relative;
  left: 0;
  height: 0;
  width: 0;
  border: 7px solid #0000;
  border-left: 13px solid white;
}
.audio-player .controls .toggle-play.play:hover {
  transform: scale(1.1);
}
.audio-player .controls .toggle-play.pause {
  height: 15px;
  width: 20px;
  cursor: pointer;
  position: relative;
}
.audio-player .controls .toggle-play.pause:before {
  position: absolute;
  top: 0;
  left: 0px;
  background: white;
  content: "";
  height: 15px;
  width: 3px;
}
.audio-player .controls .toggle-play.pause:after {
  position: absolute;
  top: 0;
  right: 8px;
  background: white;
  content: "";
  height: 15px;
  width: 3px;
}
.audio-player .controls .toggle-play.pause:hover {
  transform: scale(1.1);
}

.audio-player .controls .volume-container {
  cursor: pointer;
  position: relative;
  z-index: 2;
}
.audio-player .controls .volume-container .volume-button {
  height: 26px;
  display: flex;
  align-items: center;
}
.audio-player .controls .volume-container .volume-button .volume {
  transform: scale(0.7);
}
.audio-player .controls .volume-container .volume-slider {
  position: absolute;
  top: 15px;
  left: -3px;
  z-index: -1;
  width: 0;
  height: 15px;
  background: white;
  box-shadow: 0 0 20px #000a;
  transition: 0.25s;
}
.audio-player .controls .volume-container .volume-slider .volume-percentage {
  background: coral;
  height: 100%;
  width: 75%;
}
.audio-player .controls .volume-container:hover .volume-slider {
  left: -123px;
  width: 120px;
}
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  
  .overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .registration-card {
    width: 35vw;
    height: 39vh;
    background-color: white;
    padding: 25px;
    border-radius: 5px;
    text-align: center;
    border-radius: 25px;
    background-image: linear-gradient(to bottom, #000000, #00069f, #000000);
  }
  
  .card-div-top {
    width: 100%;
    display: flex;
    justify-content:space-between;
    align-items: center;
  }
  .card-number{
    color: white;
    width: 40%;
    text-align: left;
  }
  .card-number p {
    margin: 0;
    font-weight: 100;
    font-size: 0.8rem;
  }
  .card-number h1 {
    margin: 0;
    font-size: 1.2rem;
  }
  .card-logo-container {
    width: 30%;
    display: flex;
    justify-content: flex-end;
  }
  .card-logo {
    width: 40%;
  }

  .card-div-middle {
    margin: 5% auto;
    color: white;
    position: relative;
  }
  
  .card-div-middle .chip {
    position: absolute;
    left: 0;
    width: 12%;
  }

  .card-div-middle h3 {
    margin: 0;
    font-size: 1.3rem;
    font-weight: 200;
    color: #f4e893;
  }

  .card-div-middle button {
    width: 20%;
    font-size: 1rem;
    font-weight: 600;
    color: white;
    background-color: rgba(0,0,0,0.4);
    border : 1px solid #e7e7e7;
    border-radius : 2px;
  }

  .card-div-middle button:hover {
    
    color: black;
    background-color: rgba(255,255,255,1);
    border : 1px solid #e7e7e7;
    transition: 0.5s;
  }
  
  .card-div-bottom {
    color: white;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .cardholder-group {
    display: flex;
    width:70%;
  }
  .cardholder-name {
    text-align: left;
  }
  .cardholder-name p {
    margin: 0;
    font-weight: 100;
    font-size: 0.8rem;
  }
  .cardholder-name h2 {
    margin: 0;
    font-size: 1.2rem;
  }
  .cardholder-img-container {
    background-color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 10px;
    margin-left: 4%;
    width: 16%;
}
  
  .cardholder-img {
    width: 65%;
  }
  .validity p {
    margin: 0;
    font-weight: 100;
    font-size: 0.8rem;
  }
  
  button {
    margin-top: 10px;
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
                        /* background-image: url("./step 1.png"); */
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
                        font-size: 0.7rem;
                      }
                      .footer .footer-sub-grp .footer-head {
                        font-size:0.7rem;
 
                      }
                    }
 
  .login-container {
    position: absolute;
    right: 0;
    top: 0;
    height: 100vh;
    width: 70%; /* Adjust width as needed */
    background-color: rgb(102, 98, 98);
    transition: transform 0.5s; /* Use a smooth transition effect */
    transform: translateX(100%); /* Initially off-screen to the right */
  }
 
  .show-login {
    transform: translateX(0); /* Move on-screen */
  }
  .main{ 
    margin: 0;
    background-image:url("../components/step.jpg");
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    height: 100vh;
    width: 100vw;
    /* clip-path: polygon(0 0, 33% 0, 33% 100%, 0% 100%); */
 
 
  }
  .main .signup-button{
    width: 150px;
    height: 60px;
    position: absolute;
    right: 10vw;
    bottom: 10vw;
 
 
 
  }
  /* Other styles */
</style>