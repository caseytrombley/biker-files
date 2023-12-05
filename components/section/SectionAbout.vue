<template>
  <!-- ======= About Us Section ======= -->
  <section id="about" class="about">
    <div class="container">

      <div class="section-title">
        <h2>About Us</h2>
        <p>
          Our passion for technology drives us to explore new frontiers and harness its full potential to transform industries. With a team of highly skilled professionals, we take pride in delivering bespoke services and products that cater to the unique needs of our clients.
        </p>
      </div>

      <div class="row content">
        <div class="col-lg-6">
          <p>
            Beyond our technical expertise, what truly sets us apart is our commitment to customer satisfaction. We believe that technology should not only be groundbreaking but also user-friendly and accessible to all. Our customer-centric approach ensures that every interaction is smooth, and every solution is tailored to exceed expectations.
          </p>
          <!--              <ul>-->
          <!--                <li><i class="ri-check-double-line"></i> Ullamco laboris nisi ut aliquip ex ea commodo consequat</li>-->
          <!--                <li><i class="ri-check-double-line"></i> Duis aute irure dolor in reprehenderit in voluptate velit</li>-->
          <!--                <li><i class="ri-check-double-line"></i> Ullamco laboris nisi ut aliquip ex ea commodo consequat</li>-->
          <!--              </ul>-->
        </div>
        <div class="col-lg-6 pt-4 pt-lg-0">
          <p>
            As we continue to evolve, we remain dedicated to our core values of innovation, integrity, and excellence. Join us in this exciting journey as we shape the future through technology and forge ahead to create a world of endless possibilities.
          </p>

          <base-button animated>Learn More</base-button>

        </div>
      </div>

    </div>
  </section><!-- End About Us Section -->
</template>

<script>
import BaseButton from "~/components/base/BaseButton";
export default {
  name: 'SectionAbout',
  components: {BaseButton},
}
</script>

<style lang="scss" scoped>

</style>
