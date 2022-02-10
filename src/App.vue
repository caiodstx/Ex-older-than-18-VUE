<template>
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Can I Drive?</title>
    </head>
    <body>
      <AgeCheck />
      <Footer id="footer" />
    </body>
  </html>
</template>

<script>
import AgeCheck from "./components/AgeCheck";
import Footer from "./components/Footer";

export default {
  name: "App",
  components: {
    AgeCheck,
    Footer,
  },
};
</script>

<style lang="scss">
#footer {
  width: 100%;
  position: fixed;
  bottom: 0;
}
</style>
