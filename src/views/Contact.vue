<template>
  <div id="reference">
    <Header />
    <div class="reference-logo">Kontakt</div>
    <div class="contents">
      <div class="container">
        <div class="row">
          <div class="col-sm-6">
            <div class="col-sm-12" style="text-align: left; margin-left: 20px">
              <h3>Kontakt detalji</h3>
            </div>
            <hr />
            <div class="col-sm-12" style="text-align: left; margin-left: 20px">
              <strong style="font-size: 20px">Telefon: </strong>062/281-493
            </div>
            <div class="col-sm-12" style="text-align: left; margin-left: 20px">
              <strong style="font-size: 20px">Email: </strong>vokakop@gmail.com
            </div>
          </div>
          <div class="col-sm-6">
            <div class="col-sm-12" style="text-align: center">
              <h3>Stupite u kontakt sa nama</h3>
            </div>
            <hr />
            <form action="/about">
              <div class="row" style="padding-top: 0px">
                <div class="col-lg-6 col-sm-12">
                  <input
                    type="text"
                    id="fname"
                    name="fname"
                    placeholder="Ime"
                    class="input-style"
                    v-model="form.firstName"
                  /><br /><br />
                </div>
                <div class="col-md-6 col-sm-12" style="">
                  <input
                    type="text"
                    id="lname"
                    name="lname"
                    placeholder="Prezime"
                    class="input-style"
                    v-model="form.lastName"
                  /><br /><br />
                </div>
                <div class="col-md-6 col-sm-12" style="">
                  <input
                    type="text"
                    id="fname"
                    name="fname"
                    placeholder="Email"
                    class="input-style"
                    v-model="form.email"
                  /><br /><br />
                </div>
                <div class="col-md-6 col-sm-12" style="">
                  <input
                    type="text"
                    id="lname"
                    name="lname"
                    placeholder="Kontakt telefon"
                    class="input-style"
                    v-model="form.phone"
                  /><br /><br />
                </div>
                <div class="col-lg-12" style="text-align: center">
                  <textarea
                    id="subject"
                    name="subject"
                    placeholder="Kako možemo da vam pomognemo?"
                    style="height: 150px; width: 100%"
                    v-model="form.message"
                  ></textarea>
                </div>
                <div class="col-lg-12" style="text-align: center">
                  <input
                    type="submit"
                    value="Submit"
                    style="text-align: center; width: 100%"
                    @click.prevent="submitForm"
                  />
                </div>
              </div>
            </form>
          </div>
          <br />
        </div>
      </div>
      <hr />
    </div>
    <Footer />
  </div>
</template>

<script>
import queryString from "query-string";
import axios from "axios";
//components
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
//pictures
import Logo1 from "@/assets/images/workers.jpg";
import Logo2 from "@/assets/images/promont.png";
import Logo3 from "@/assets/images/millennium_logo.png";
import Logo4 from "@/assets/images/setec.png";

export default {
  name: "Home",
  data() {
    return {
      mobileView: true,
      showNav: true,
      slideOne: Logo1,
      slideTwo: Logo2,
      slideThree: Logo3,
      slideFour: Logo4,
      displayPhoto: Logo1,
      displayPhotoAlt: "Prvi",
      form: {
        firstName: "",
        lastName: "",
        email: "",
        phone: "",
        message: "",
      },
      errors: [],
    };
  },
  components: {
    Header,
    Footer,
  },
  methods: {
    handleView() {
      this.mobileView = window.innerWidth <= 990;
    },
    toggleShowNav() {
      this.showNav = !this.showNav;
    },
    redirectOne() {
      window.location.href = "https://kabelnetgroup.com/";
    },
    redirectTwo() {
      window.location.href = "https://www.promontgroup.rs/";
    },
    redirectThree() {
      window.location.href = "https://www.millenniumteam.rs/sr";
    },
    redirectFour() {
      window.location.href = "http://www.setec-ec.rs/";
    },
    changePictureOne() {
      this.displayPhoto = this.slideOne;
      this.displayPhotoAlt = "Prvi";
    },
    changePictureTwo() {
      this.displayPhoto = this.slideTwo;
      this.displayPhotoAlt = "Drugi";
    },
    changePictureThree() {
      this.displayPhoto = this.slideThree;
      this.displayPhotoAlt = "Treći";
    },
    changePictureFour() {
      this.displayPhoto = this.slideFour;
      this.displayPhotoAlt = "Cetvrti";
    },
    async submitForm() {
      console.log(this.form);
      await axios
        .post(
          "https://www.vokakop.com/mailerApp.php",
          queryString.stringify(this.form)
        )
        .then(() => {
          alert("Form submitted successfully");
          this.errors = [];
        })
        .catch((error) => {
          alert("The form has errors");
          this.errors = error.response.data.message;
        });
    },
  },

  created() {
    this.handleView();
  },
};
</script>
<style>
@import url("https://use.fontawesome.com/releases/v5.9.0/css/all.css");
* {
  font-size: 1rem;
}
body {
  width: 100%;
  height: 100%;
  padding: 0;
  font-family: "Segoe UI", Tahoma;
  background-color: #231f20;
}
.input-style {
  width: 100%;
}
#reference {
  width: 100%;
  height: 100%;
}
.contents {
  position: relative;
  width: 100%;
  background-color: white;
  padding: 20px;
  height: 100%;
}
.slider {
  width: 100%;
  height: 410px;
  padding: 5px;
  background-color: white;
  overflow: hidden;
}
.reference-logo {
  position: relative;
  width: 100%;
  background: linear-gradient(rgba(255, 0, 0, 0), #231f20);
  font-size: 6vh;
  padding-top: 100px;
  text-align: center;
  color: #fff;
  height: 310px;
}
.partners-logo {
  object-fit: contain;
  width: 100%;
  height: 320px;
  text-align: center;
  background: linear-gradient(#231f20 15%, #fff);
}
br {
  border: 1px solid #ff5858;
  background: #fff;
}
.Reference-slide {
  position: relative;
  color: #fff;
  background: #fff;
  width: 100%;
  z-index: 1;
  font-family: Arial;
  font-size: 24px;
  text-align: center;
  min-height: 50px;
}
.logoSlika {
  object-fit: contain;
  width: 100%;
  padding: 5px;
  height: 100px;
  cursor: pointer;
}
.display-image {
  width: 100%;
  border: 2px solid black;
  height: 400px;
  object-fit: contain;
}
#display-menu {
  height: 120px;
  object-fit: contain;
  width: 95%;
  border: 2px solid black;
}
.photoAlt {
  background-color: black;
  color: white;
  opacity: 0.3;
  width: 100%;
  border-bottom-left-radius: 5px;
  border-bottom-right-radius: 5px;
  text-align: left;
  padding: 5px;
}
.col-sm-6 {
  flex-direction: column;
}
</style>
