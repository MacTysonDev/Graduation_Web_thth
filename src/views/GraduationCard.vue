<template>
  <div id="background" class="d-flex justify-content-center align-items-center p-0 m-0">
    <div id="card_box" class="px-5 py-3 text-center d-flex justify-content-center align-items-center">
      <div id="content" class="d-flex flex-column justify-content-between">
        <div id="content_header" class="pb-3 d-flex align-items-center justify-content-center">
          <img src="../assets/bear_ani.gif" class="header_img">
          <img src="../assets/bear_ani.gif" class="header_img">
          <img src="../assets/bear_ani.gif" class="header_img">
        </div>
        <div id="greeting">
          <h6 class="mb-4">THÂN MỜI BẠN ĐẾN THAM DỰ</h6>
          <h3 class="my-4" style="font-weight: 800;">LỄ TỐT NGHIỆP</h3>
          <h5 class="mb-3"style="font-weight: 500;">CỦA THANH THẢO</h5>
        </div>
        <div id="content_center" class="mt-2">
          <img src="../assets/uni_logo1.png" class="logo_img">
        </div>
        <div id="content_footer" class="mb-5">
          <template v-if="isMobile">
            <h2 class="my-4">{{ userName }}</h2>
            <div id="info_box" class="d-flex flex-column mb-3">
              <div class="info_content">
                <span>09.08.2024</span> / <span>14:00 PM</span>
              </div>
              <div class="info_content">
                <div>Hội trường A8</div>
                <div>Trường Đại học Hàng hải Việt Nam</div>
              </div>
            </div>
            <h6 style="font-weight: 600;">THÔNG TIN LIÊN HỆ 0355168336</h6>
          </template>
          <template v-else>
            <h2 class="my-4">{{ userName }}</h2>
            <div id="info_box" class="d-flex justify-content-between mb-3"> 
              <div class="info_content col-md-6">
                <div>Thứ sáu</div>
                <div>09.08.2024</div>
                <div>14:00 PM</div>
              </div>
              <div class="info_content col-md-6">
                <div>Hội trường A8</div>
                <div>Trường Đại học Hàng hải Việt Nam</div>
              </div>
            </div>
            <h6 style="font-weight: 600;">THÔNG TIN LIÊN HỆ 0355168336</h6>
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'

export default {
  setup() {
    const userName = ref(localStorage.getItem('userName'))
    const isMobile = ref(window.innerWidth <= 786)

    const createFallingLeaves = () => {
      const container = document.getElementById('background')
      const leafCount = 40 // số lượng lá phong

      for (let i = 0; i < leafCount; i++) {
        const leaf = document.createElement('div')
        leaf.className = 'maple-leaf'
        leaf.style.left = `${Math.random() * 100}vw`
        leaf.style.top = `-${Math.random() * 130}vh` // Khởi tạo từ phía trên đỉnh trang
        leaf.style.animationDuration = `${2 + Math.random() * 4}s` // Thời gian chạy animation
        leaf.style.animationDelay = `${Math.random() * 5}s`
        container.appendChild(leaf)

        // Xóa lá sau khi hoàn thành animation
        leaf.addEventListener('animationend', () => {
          leaf.remove()
        })
      }
    }

    onMounted(() => {
      document.title = 'Graduation Card'
      createFallingLeaves()

      // Cập nhật giá trị isMobile khi kích thước cửa sổ thay đổi
      const updateMobileStatus = () => {
        isMobile.value = window.innerWidth <= 786
      }
      window.addEventListener('resize', updateMobileStatus)
    })

    return {
      userName,
      isMobile
    }
  }
}
</script>


<style>
/* Phần CSS hiện có */
#background {
  background-color: #FACDE5;
  padding: 20px;
  height: 100vh;
  overflow: hidden; /* Đảm bảo không hiển thị thanh cuộn khi lá rơi */
  position: relative;
}
/* Phần CSS của các ảnh và thông tin khác */
#card_box {
  background-image: url('../assets/bow_border.png');
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  width: 478px;
  height: 700px;
  z-index: 10; /* Đảm bảo card_box có z-index lớn */
  position: relative; /* Thêm position để z-index hoạt động */
}
.header_img {
  width:60px; 
  height: auto;
}
.border_img {
  width: 100px;
  height: 100px;
}
.logo_img {
  width: 150px;
  height: 150px;
} 
.info_content {
  text-transform: uppercase;
  font-size: 11pt;
}
/* CSS cho lá phong */
.maple-leaf {
  position: absolute;
  width: 30px;
  height: 30px;
  background-image: url('../assets/star.gif'); /* Đảm bảo đường dẫn đúng */
  background-size: cover;
  animation: fall linear infinite;
  pointer-events: none;
  z-index: 5; /* Đảm bảo lá phong có z-index nhỏ */
}

@keyframes fall {
  0% {
    transform: translateY(0) rotate(0deg);
    opacity: 1;
  }
  100% {
    transform: translateY(100vh) rotate(360deg);
    opacity: 0;
  }
}

/* Responsive */
@media (max-width: 786px) {
  #card_box {
    width: 100%;
    height: auto; /* Để vừa với nội dung trên màn hình nhỏ */
    background-image: none;
  }

  #content_footer {
    text-align: center;
  }

  .info_content {
    font-size: 10pt; /* Giảm kích thước chữ cho màn hình nhỏ hơn */
  }
}
@media (max-width: 480px) {
  #card_box {
    padding: 5vw;
  }

  .info_content {
    font-size: 4vw;
  }
}
/* @media (max-width: 1536px) {
  #card_box {
    width: 50%;
    height: auto;
    padding: 20px;
  }

  .logo_img {
    width: 120px;
    height: 120px;
  }

  .info_content {
    font-size: 12pt;
  }
}  */

</style>