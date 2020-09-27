<template>
  <div class="flex flex-col justify-center h-screen">
    <img
      alt="DSC logo"
      class="dsc-logo mx-0 pl-4 pt-4 hidden md:block"
      src="~assets/dsclogo.png"
    />
    <img
      alt="DSC logo"
      class="dsc-logo mx-auto mt-4 md:pl-4 md:pt-4 md:hidden"
      src="~assets/dsclogo-mobile.png"
    />

    <div class="vertical-center">
      <div class="hades-banner flex flex-col items-center">
        <img
          alt="Hades logo"
          class="mr-auto ml-auto"
          src="~assets/hadeslogo.png"
        />
        <div class="text-3xl md:text-4xl font-bold">Project Hades</div>
      </div>

      <div class="flex justify-center flex-wrap mt-4 md:mt-12 pr-8 pl-8">
        <label for="email-input" class="py-2 hidden md:block">Email ID:</label>
        <input
          id="email-input"
          v-model="emailInput"
          type="email"
          placeholder="john.doe@example.com"
          :class="{ border: inputError }"
          class="rounded-md outline-none pl-3 pr-20 py-3 sm:py-0 sm:ml-4 text-xs border-red-500"
        />

        <span class="inline-flex rounded-md shadow-sm">
          <button
            class="inline-flex items-center submit-btn outline-none text-white text-sm px-4 py-2 mt-4 sm:mt-0 sm:ml-8 rounded-md"
            @click="handleSubmit"
          >
            <svg
              v-if="isLoading"
              class="animate-spin -ml-1 mr-3 h-5 w-5 text-white"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
            >
              <circle
                class="opacity-25"
                cx="12"
                cy="12"
                r="10"
                stroke="currentColor"
                stroke-width="4"
              />
              <path
                class="opacity-75"
                fill="currentColor"
                d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
              />
            </svg>
            Register for beta access!
          </button>
        </span>
      </div>
    </div>
    <div
      class="flex justify-center w-50 mt-auto pl-4 pr-4 pb-5 md:pl-8 md:pr-8 md:pb-6"
    >
      <a class="mx-4 md:mx-16" href="https://www.facebook.com/dscvitvellore/">
        <img class="h-auto w-8" src="~assets/facebook.svg" />
      </a>
      <a class="mx-4 md:mx-16" href="https://www.instagram.com/dscvitvellore/">
        <img class="h-auto w-8" src="~assets/instagram.svg" />
      </a>
      <a class="mx-4 md:mx-16" href="https://twitter.com/dscvit">
        <img class="h-auto w-8" src="~assets/twitter.svg" />
      </a>
      <a class="mx-4 md:mx-16" href="https://www.linkedin.com/company/dscvit/">
        <img class="h-auto w-8" src="~assets/linkedin.svg" />
      </a>
    </div>

    <ErrorModal
      :show="showErrorModal"
      :text="modalText"
      @close="handleModalClosed"
    />
    <SuccessModal
      :show="showSuccessModal"
      :text="modalText"
      @close="handleModalClosed"
    />
  </div>
</template>

<script>
const isValidEmail = (mail) =>
  /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/.test(
    mail
  )

export default {
  name: 'Home',
  data() {
    return {
      showErrorModal: false,
      showSuccessModal: false,
      modalText: '',
      emailInput: '',
      inputError: false,
      isLoading: false,
    }
  },
  methods: {
    async handleSubmit() {
      if (isValidEmail(this.emailInput)) {
        this.inputError = false
        try {
          this.isLoading = true
          const response = await this.$axios.post(
            'https://hades-beta-backend.herokuapp.com/email',
            { email: this.emailInput }
          )
          if (response.status === 201) {
            this.showSuccessModal = true
            this.modalText =
              "Thank you for registering for the beta of Project Hades! We'll send you a mail when the beta is up and running."
            this.emailInput = ''
          }
        } catch (err) {
          this.inputError = true
          this.showErrorModal = true
          if (err.response.status === 409) {
            this.modalText =
              'This account is already registered. Try again with a different account.'
          } else {
            this.modalText = err.response.data.msg
          }
        }
        this.isLoading = false
      } else {
        this.inputError = true
      }
    },

    handleModalClosed() {
      this.showErrorModal = false
      this.showSuccessModal = false
      this.modalText = ''
    },
  },
}
</script>

<style>
.dsc-logo {
  width: 400px;
  height: auto;
}

.vertical-center {
  margin: 0;
  position: absolute;
  width: 100%;
  top: 45%;
  left: 50%;
  -ms-transform: translate(-50%, -45%);
  transform: translate(-50%, -45%);
}

.hades-banner img {
  width: 200px;
  height: auto;
}

#email-input {
  background-color: #f5f8fd;
}

.submit-btn {
  background-color: #2685fb;
  outline: none;
}

.submit-btn:focus {
  outline: none;
}

a {
  cursor: pointer;
  text-decoration: none;
}

.loader {
  border-top-color: green;
  -webkit-animation: spinner 1.5s linear infinite;
  animation: spinner 1.5s linear infinite;
}

@-webkit-keyframes spinner {
  0% {
    -webkit-transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(360deg);
  }
}

@keyframes spinner {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
