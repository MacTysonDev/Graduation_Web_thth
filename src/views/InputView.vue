<template>
  <div id="background" class="d-flex justify-content-center align-items-center p-0 m-0">
    <div id="input_box" class="p-5 text-center d-flex justify-content-between align-items-center">
      <div id="content" class="d-flex flex-column justify-content-between">
        <div id="content_header">
        </div>
        <div id="greeting">
          <h2 class="mb-4" style="line-height: 50px;">CHÀO MỪNG ĐẾN VỚI TRANG WEB</h2> 
          <img src="../assets/heart_rotating.gif" style="width:120px; height: auto;" alt="">
        </div>
        <div id="content_center">
          <h4>
            Hãy nhập tên của bạn vào đây nhé<br> 
            <img src="../assets/bear_icon.png" class="icon_input p-2">
            <img src="../assets/bear_icon.png" class="icon_input p-2">
            <img src="../assets/bear_icon.png" class="icon_input p-2">
          </h4>
          <input type="text" class="form-control mb-4" v-model="userName" @focus="playMusic">
          <router-link class="button-input btn mt-3 px-5 py-2" @click="checkInput" to="/graduation-card"> 
            Gửi <i class="fa-solid fa-paper-plane"></i>
          </router-link>
        </div>
        <div id="content_footer">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue';
import Swal from 'sweetalert2';
import { userStore } from '../stores/store';
import router from '../routers/router';

export default {
  setup() {
    const userName = ref('');
    const userStoreName = userStore();
    const audio = ref(null);

    const savedName = localStorage.getItem('userName');
    if (savedName) {
      userStoreName.setUserName(savedName);
    }


    const checkInput = () => {
      if (userName.value === '') {
        Swal.fire({
          icon: 'error',
          title: 'Oops...',
          text: 'Vui lòng nhập tên của bạn!',
        });
        router.push('/');
      } else {
        localStorage.setItem('userName', userName.value);
        userStoreName.setUserName(userName.value);
      }
    }

  onMounted(() => {
    document.title = 'Welcome';
  });

    return {
      userName,
      checkInput
    }
  }
}
</script>

<style scoped>
#background {
  background-color: #facde5;
  padding: 20px;
  height: 100vh;
}
#input_box {
  border: 1px solid #434634;
  border-radius: 28px;
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  width: 520px;
  height: 686px;
}
#input_box h3 {
  color: #434634;
}
#input_box input {
  width: 100%;
  border: none;
  border-bottom: 1px solid #434634;
  background-color: transparent;
  margin-top: 20px;
}
#input_box .button-input {
  border: none;
  border-radius: 8px;
  background-color: #FF647F;
  color: white;
  transition: 0.25s;
}
#input_box .button-input:hover {
  background-color: #FFC0CB;
  color: #FF647F;
}
.icon_input{
  width: 60px;
  height: auto;
}
#content {
  width: 100%;
  height: 100%;
}
#content_header .bow {
  width: 100px;
  height: auto;
}
#content_header .creeper_tree {
  width: 150px;
  height: auto;
}

/* Responsive */
@media (max-width: 786px) {
  #input_box {
    width: 100%;
    height: auto; /* Để vừa với nội dung trên màn hình nhỏ */
    background-image: none;
  }
  .creeper_tree, .bow {
    width: 50px;
  }
  #content_footer {
    text-align: center;
  }

  .info_content {
    font-size: 10pt; /* Giảm kích thước chữ cho màn hình nhỏ hơn */
  }
}
@media (max-width: 480px) {
  #input_box {
    padding: 5vw;
  }
  #content_header .creeper_tree, #content_header .bow {
    width: 20vw;
    margin-bottom: 20px;
  }
  .info_content {
    font-size: 4vw;
  }
} 
</style>