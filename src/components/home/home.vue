<template>
  <div class="home-container flex flex-col justify-center">
    <img
      alt="DSC logo"
      class="dsc-logo mr-0 ml-0 pl-4 pt-4 hidden md:block"
      src="../../assets/dsclogo.png"
    />
    <img
      alt="DSC logo"
      class="dsc-logo mr-auto ml-auto mt-4 md:pl-4 md:pt-4 md:hidden"
      src="../../assets/dsclogo-mobile.png"
    />

    <div class="vertical-center">
      <div class="hades-banner flex flex-col items-center">
        <img alt="Hades logo" class="mr-auto ml-auto" src="../../assets/hadeslogo.png" />
        <div class="text-3xl md:text-4xl font-bold">Project Hades</div>
      </div>

      <div class="flex justify-center flex-wrap mt-4 md:mt-12 pr-8 pl-8">
        <label for="email-input" class="pt-2 pb-2 hidden md:block">Email ID:</label>
        <input
          type="text"
          placeholder="john.doe@example.com"
          id="email-input"
          class="rounded-md pl-3 pr-20 pb-3 pt-3 md:pb-0 md:pt-0 md:ml-4 text-xs"
        />
        <button
          class="submit-btn text-white text-sm pl-8 pr-8 pt-2 pb-2 mt-4 md:mt-0 sm:ml-8 mb-auto rounded-md"
        >Register for beta access!</button>
      </div>
    </div>
    <div class="flex justify-between mt-auto pl-4 pr-4 pb-5 md:pl-8 md:pr-8 md:pb-6">
      <a class="ml-2 mr-2" href="https://www.facebook.com/dscvitvellore/">
        <img class="h-auto w-8" src="../../assets/facebook.svg" />
      </a>
      <a class="ml-2 mr-2" href="https://www.instagram.com/dscvitvellore/">
        <img class="h-auto w-8" src="../../assets/instagram.svg" />
      </a>
      <a class="ml-2 mr-2" href="https://twitter.com/dscvit">
        <img class="h-auto w-8" src="../../assets/twitter.svg" />
      </a>
      <a class="ml-2 mr-2" href="https://www.linkedin.com/company/dscvit/">
        <img class="h-auto w-8" src="../../assets/linkedin.svg" />
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
};
</script>

<style>
@import "./home.css";
</style>
