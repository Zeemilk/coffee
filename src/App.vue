<script setup>
import { ref } from 'vue'

const coffeeshops = ref([
  {
    name: "Amazon Cafe",
    img: "https://www.cafe-amazon.com/images/logo.png",
    price: 60,
    description: "จากนกแก้ว",
    web: "https://www.cafe-amazon.com/index.aspx"
  },
  {
    name: "Choi Doi",
    img: "http://www.chaodoicoffee.com/public/library/images/200x200/1421251622.png",
    price: 40,
    description: "จากชาวดอย",
    web: "http://www.chaodoicoffee.com/"
  },
  {
    name: "Starbuck",
    img: "https://www.starbucks.co.th/stb-media/2020/10/starbucks_corporation_logo.png",
    price: 95,
    description: "จากสตาร์บัค",
    web: "https://www.starbucks.co.th/th/"
  },
  {
    name: "Red Diamond",
    img: "https://scontent.fcnx3-1.fna.fbcdn.net/v/t39.30808-6/327170229_535824744999232_6302688726097934756_n.jpg?_nc_cat=102&ccb=1-7&_nc_sid=a2f6c7&_nc_eui2=AeFgSpfnI4IQnSklExZeX0HGgcTUa8DFl0KBxNRrwMWXQnJ_O4AXp1sHcA1vbD83ChcgzTuKtTKzbMUZBUUx8jDy&_nc_ohc=akwcZk-6PN8AX_Bf5Xz&_nc_ht=scontent.fcnx3-1.fna&oh=00_AfAOLjfpIsw60MaMrdOb9tPaxWm6L79aVChpajJKLdnpbg&oe=6509FE14",
    price: 120,
    description: "จากเพชรแดง",
    web: "https://www.facebook.com/Reddiamondthailand/"
  },
  {
    name: "Inthanin",
    img: "https://www.inthanincoffee.com/img/logo/logo@2x.png?1482390380",
    price: 35,
    description: "จากอินทนิล",
    web: "https://www.inthanincoffee.com/"
  },
  {
    name: "Blue Cup",
    img: "https://scontent.fcnx3-1.fna.fbcdn.net/v/t39.30808-6/347388946_797149818690710_792332344402018362_n.png?_nc_cat=101&ccb=1-7&_nc_sid=a2f6c7&_nc_eui2=AeEaZ_4CIuWC-CuSTRjuhTTpTSB5_7AI_JtNIHn_sAj8m9wx5UwoPgAOXjEQ0C2qY3qQI8oYu-jiYKZvG1xLxXn2&_nc_ohc=zqF6ABBCZfUAX83_zZs&_nc_ht=scontent.fcnx3-1.fna&oh=00_AfCpDVLY_Gl3nHyXI4Nd6rqzlBmc7f5LNdTVlRuMTZBNSw&oe=65095D02",
    price: 75,
    description: "จากแก้วฟ้า",
    web: "https://www.facebook.com/bluecup/"
  }
]);

const bookingData = ref({
  name: '',
  phone: '',
  date: '',
  time: '',
  tableCount: 0,
});

const bookingDialog = ref(false); 
const reserve = () => {
  bookingDialog.value = true;
};

const confirmBooking = () => {
  if (isValidBookingData(bookingData.value)) {
    performBooking(bookingData.value);

    bookingDialog.value = false;
    bookingSuccess.value = true;
  } else {
    console.error("ข้อมูลการจองไม่ถูกต้อง");
  }
};

const isValidBookingData = (data) => {

  return (
    data.name !== '' &&
    data.phone !== '' &&
    data.date !== '' &&
    data.time !== '' &&
    data.tableCount > 0
  );
};

const performBooking = (data) => {
  console.log("จองข้อมูล:", data);
};
const bookingSuccess = ref(false);

const closeBookingSuccess = () => {
  bookingSuccess.value = false;
};


</script>

<template>
  <v-card max-width="500" class="mx-auto" color="grey-lighten-3">
    <v-layout>
      <v-app-bar
        color="teal-darken-4"
        image="https://t4.ftcdn.net/jpg/01/35/34/59/360_F_135345906_DBaCFikNHgOMH7owi8wcuRXN0phu2xs6.jpg"
      >
        <template v-slot:image>
          <v-img
            gradient="to top right, rgba(19,84,122,.8), rgba(128,208,199,.8)"
          ></v-img>
        </template>

        <template v-slot:prepend>
          <v-app-bar-nav-icon></v-app-bar-nav-icon>
        </template>

        <v-app-bar-title><RouterLink to="/">Home</RouterLink>  <RouterLink to="/about">About</RouterLink></v-app-bar-title>

        <v-spacer></v-spacer>

        <v-btn icon>
          <v-icon>mdi-magnify</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-heart</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </v-app-bar>
    </v-layout>
    
    <v-layout align-center justify-center>
      <div v-for="(shop) in coffeeshops.slice(0, 3)" :key="shop.name" class="shop-card-top">
        <img class="shop-card-img" :src="shop.img" alt="ร้านกาแฟ">
        <h2>{{ shop.name }}</h2>
        <p>ราคา: {{ shop.price }} บาท</p>
        <p>{{ shop.description }}</p>
        <a v-if="shop.web" :href="shop.web" target="_blank">เว็บไซต์</a>
        <v-btn @click="reserve(shop)">จอง</v-btn>
      </div>   
    </v-layout>
    <v-layout align-center justify-center>
      <div v-for="(shop) in coffeeshops.slice(3, 6)" :key="shop.name" class="shop-card-bottom">
        <img class="shop-card-img" :src="shop.img" alt="ร้านกาแฟ">
        <h2>{{ shop.name }}</h2>
        <p>ราคา: {{ shop.price }} บาท</p>
        <p>{{ shop.description }}</p>
        <a v-if="shop.web" :href="shop.web" target="_blank">เว็บไซต์</a>
        <v-btn @click="reserve(shop)">จอง</v-btn>
      </div>
    </v-layout> 
  </v-card>

  <v-dialog v-model="bookingDialog" max-width="400px">
        <v-card>
          <v-card-title>กรอกข้อมูลการจอง</v-card-title>
          <v-card-text>
            <v-text-field v-model="bookingData.name" label="ชื่อ"></v-text-field>
            <v-text-field v-model="bookingData.phone" label="เบอร์โทร"></v-text-field>
            <v-text-field v-model="bookingData.date" label="วันที่"></v-text-field>
            <v-text-field v-model="bookingData.time" label="เวลา"></v-text-field>
            <v-text-field v-model="bookingData.tableCount" label="จำนวนโต๊ะ" type="number"></v-text-field>
          </v-card-text>
          <v-card-actions>
            <v-btn color="red" @click="bookingDialog = false">ยกเลิก</v-btn>
            <v-btn color="green" @click="confirmBooking">ยืนยัน</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>

      <v-dialog v-model="bookingSuccess" max-width="400px">
    <v-card>
      <v-card-title>การจองสำเร็จ</v-card-title>
      <v-card-text>
        <p>ข้อมูลการจอง:</p>
        <ul>
          <li><strong>ชื่อ:</strong> {{ bookingData.name }}</li>
          <li><strong>เบอร์โทร:</strong> {{ bookingData.phone }}</li>
          <li><strong>วันที่:</strong> {{ bookingData.date }}</li>
          <li><strong>เวลา:</strong> {{ bookingData.time }}</li>
          <li><strong>จำนวนโต๊ะ:</strong> {{ bookingData.tableCount }}</li>
        </ul>
      </v-card-text>
      <v-card-actions>
        <v-btn color="primary" @click="closeBookingSuccess">ปิด</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
 
</template>
<style scoped>
.shop-card-top{
  background-color: #266421;
  margin: 10px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  text-align: center;
  margin-right: 10px; 
  margin-top: 80px;  
  text-align: center;
}
.shop-card-bottom{
  background-color: #266421;
  margin: 10px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  text-align: center;
  margin-right: 10px; 
}
.shop-card-img {
  max-width: 100px;
  max-height: 200px;
}
</style>
