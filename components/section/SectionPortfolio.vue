<template>
  <section id="portfolio" class="portfolio">
    <div class="container">

      <div class="section-title">
        <h2>Portfolio</h2>
        <p>
          Browse through our projects to witness the fusion of innovation and craftsmanship. We're excited to share our work with you and look forward to collaborating on your next venture
        </p>
      </div>

      <div class="row">
        <div class="col-lg-12 d-flex justify-content-center">
          <ul id="portfolio-filters">
            <li data-filter="*" class="filter-active">All</li>
            <li data-filter=".filter-app">App</li>
            <li data-filter=".filter-card">Card</li>
            <li data-filter=".filter-web">Web</li>
          </ul>
        </div>
      </div>

      <div class="row portfolio-container">

        <div v-for="(item, i) in portfolio" :key="i" class="col-lg-4 col-md-6 portfolio-item filter-app">
          <detail-card
              :title="item.title"
              :description="item.description"
              :detailedDescription="item.detailedDescription"
              :image="item.slides[0].image"
              :slides="item.slides"
          />

        </div>



      </div>

      <!--          <div class="row portfolio-container">-->

      <!--            <div class="col-lg-4 col-md-6 portfolio-item filter-app">-->
      <!--              <video src="assets/video/portfolio/portfolio-1.jpg" class="video-fluid" alt="">-->
      <!--              <div class="portfolio-info">-->
      <!--                <h4>App 1</h4>-->
      <!--                <p>App</p>-->
      <!--                <a href="assets/video/portfolio/portfolio-1.jpg" data-gallery="portfolioGallery" class="portfolio-lightbox preview-link" title="App 1"><i class="bx bx-plus"></i></a>-->
      <!--                <a href="portfolio-details.html" class="details-link" title="More Details"><i class="bx bx-link"></i></a>-->
      <!--              </div>-->
      <!--            </div>-->

      <!--            <div class="col-lg-4 col-md-6 portfolio-item filter-web">-->
      <!--              <video src="assets/video/portfolio/portfolio-2.jpg" class="video-fluid" alt="">-->
      <!--              <div class="portfolio-info">-->
      <!--                <h4>Web 3</h4>-->
      <!--                <p>Web</p>-->
      <!--                <a href="assets/video/portfolio/portfolio-2.jpg" data-gallery="portfolioGallery" class="portfolio-lightbox preview-link" title="Web 3"><i class="bx bx-plus"></i></a>-->
      <!--                <a href="portfolio-details.html" class="details-link" title="More Details"><i class="bx bx-link"></i></a>-->
      <!--              </div>-->
      <!--            </div>-->

      <!--            <div class="col-lg-4 col-md-6 portfolio-item filter-app">-->
      <!--              <video src="assets/video/portfolio/portfolio-3.jpg" class="video-fluid" alt="">-->
      <!--              <div class="portfolio-info">-->
      <!--                <h4>App 2</h4>-->
      <!--                <p>App</p>-->
      <!--                <a href="assets/video/portfolio/portfolio-3.jpg" data-gallery="portfolioGallery" class="portfolio-lightbox preview-link" title="App 2"><i class="bx bx-plus"></i></a>-->
      <!--                <a href="portfolio-details.html" class="details-link" title="More Details"><i class="bx bx-link"></i></a>-->
      <!--              </div>-->
      <!--            </div>-->

      <!--            <div class="col-lg-4 col-md-6 portfolio-item filter-card">-->
      <!--              <video src="assets/video/portfolio/portfolio-4.jpg" class="video-fluid" alt="">-->
      <!--              <div class="portfolio-info">-->
      <!--                <h4>Card 2</h4>-->
      <!--                <p>Card</p>-->
      <!--                <a href="assets/video/portfolio/portfolio-4.jpg" data-gallery="portfolioGallery" class="portfolio-lightbox preview-link" title="Card 2"><i class="bx bx-plus"></i></a>-->
      <!--                <a href="portfolio-details.html" class="details-link" title="More Details"><i class="bx bx-link"></i></a>-->
      <!--              </div>-->
      <!--            </div>-->

      <!--            <div class="col-lg-4 col-md-6 portfolio-item filter-web">-->
      <!--              <video src="assets/video/portfolio/portfolio-5.jpg" class="video-fluid" alt="">-->
      <!--              <div class="portfolio-info">-->
      <!--                <h4>Web 2</h4>-->
      <!--                <p>Web</p>-->
      <!--                <a href="assets/video/portfolio/portfolio-5.jpg" data-gallery="portfolioGallery" class="portfolio-lightbox preview-link" title="Web 2"><i class="bx bx-plus"></i></a>-->
      <!--                <a href="portfolio-details.html" class="details-link" title="More Details"><i class="bx bx-link"></i></a>-->
      <!--              </div>-->
      <!--            </div>-->

      <!--            <div class="col-lg-4 col-md-6 portfolio-item filter-app">-->
      <!--              <video src="assets/video/portfolio/portfolio-6.jpg" class="video-fluid" alt="">-->
      <!--              <div class="portfolio-info">-->
      <!--                <h4>App 3</h4>-->
      <!--                <p>App</p>-->
      <!--                <a href="assets/video/portfolio/portfolio-6.jpg" data-gallery="portfolioGallery" class="portfolio-lightbox preview-link" title="App 3"><i class="bx bx-plus"></i></a>-->
      <!--                <a href="portfolio-details.html" class="details-link" title="More Details"><i class="bx bx-link"></i></a>-->
      <!--              </div>-->
      <!--            </div>-->

      <!--            <div class="col-lg-4 col-md-6 portfolio-item filter-card">-->
      <!--              <video src="assets/video/portfolio/portfolio-7.jpg" class="video-fluid" alt="">-->
      <!--              <div class="portfolio-info">-->
      <!--                <h4>Card 1</h4>-->
      <!--                <p>Card</p>-->
      <!--                <a href="assets/video/portfolio/portfolio-7.jpg" data-gallery="portfolioGallery" class="portfolio-lightbox preview-link" title="Card 1"><i class="bx bx-plus"></i></a>-->
      <!--                <a href="portfolio-details.html" class="details-link" title="More Details"><i class="bx bx-link"></i></a>-->
      <!--              </div>-->
      <!--            </div>-->

      <!--            <div class="col-lg-4 col-md-6 portfolio-item filter-card">-->
      <!--              <video src="assets/video/portfolio/portfolio-8.jpg" class="video-fluid" alt="">-->
      <!--              <div class="portfolio-info">-->
      <!--                <h4>Card 3</h4>-->
      <!--                <p>Card</p>-->
      <!--                <a href="assets/video/portfolio/portfolio-8.jpg" data-gallery="portfolioGallery" class="portfolio-lightbox preview-link" title="Card 3"><i class="bx bx-plus"></i></a>-->
      <!--                <a href="portfolio-details.html" class="details-link" title="More Details"><i class="bx bx-link"></i></a>-->
      <!--              </div>-->
      <!--            </div>-->

      <!--            <div class="col-lg-4 col-md-6 portfolio-item filter-web">-->
      <!--              <video src="assets/video/portfolio/portfolio-9.jpg" class="video-fluid" alt="">-->
      <!--              <div class="portfolio-info">-->
      <!--                <h4>Web 3</h4>-->
      <!--                <p>Web</p>-->
      <!--                <a href="assets/video/portfolio/portfolio-9.jpg" data-gallery="portfolioGallery" class="portfolio-lightbox preview-link" title="Web 3"><i class="bx bx-plus"></i></a>-->
      <!--                <a href="portfolio-details.html" class="details-link" title="More Details"><i class="bx bx-link"></i></a>-->
      <!--              </div>-->
      <!--            </div>-->

      <!--          </div>-->

    </div>
  </section>
</template>

<script>
import DetailCard from "~/components/DetailCard";
export default {
  name: 'SectionPortfolio',
  components: {DetailCard},
  data() {
    return {
      portfolio: [
        {
          title: 'Dereva',
          description: 'Integrated solutions',
          detailedDescription: 'Our platform brings together a range of essential business functions into one centralized hub, enabling you to streamline workflows, eliminate data silos, and make informed decisions with ease.',
          image: 'video/portfolio/portfolio-image-dereva.jpg',
          slides: [
            {
              image: 'video/portfolio/portfolio-image-dereva.jpg',
              alt: '',
              title: '',
              description: '',
            },
          ],
        },
        {
          title: 'Hadithi',
          description: 'The story of Africa',
          detailedDescription: 'Web application that offers literature about the history and traditions of the many tribes in Africa.',
          image: 'video/portfolio/portfolio-image-hadithi.jpg',
          slides: [
            {
              image: 'video/portfolio/portfolio-image-hadithi.jpg',
              alt: '',
              title: '',
              description: '',
            },
          ],
        },
        {
          title: 'Thome Images',
          description: 'Rare and authentic photography',
          detailedDescription: 'Thome Images provides authentic and fully licensed photographs and prints of tribalism, religion, and rare wonders of the natural world. These vintage photos give a glimpse into the customs of world culture.',
          image: 'video/portfolio/portfolio-image-thome-images.jpg',
          slides: [
            {
              image: 'video/portfolio/portfolio-image-thome-images.jpg',
              alt: '',
              title: '',
              description: '',
            },
          ],
        },
        {
          title: 'Mpishi',
          description: 'Unique and authentic recipes',
          detailedDescription: 'Mpishi is a site for sharing unique and authentic recipes.',
          image: 'video/portfolio/portfolio-image-mpishi.jpg',
          slides: [
            {
              image: 'video/portfolio/portfolio-image-mpishi.jpg',
              alt: '',
              title: '',
              description: '',
            },
            {
              image: 'video/portfolio/portfolio-image-mpishi-2.jpg',
              alt: '',
              title: '',
              description: '',
            },
            {
              image: 'video/portfolio/portfolio-image-mpishi-3.jpg',
              alt: '',
              title: '',
              description: '',
            },
            {
              image: 'video/portfolio/portfolio-image-mpishi-4.jpg',
              alt: '',
              title: '',
              description: '',
            },
            {
              image: 'video/portfolio/portfolio-image-mpishi-5.jpg',
              alt: '',
              title: '',
              description: '',
            },
          ],
        },
      ]
    }
  }
}
</script>

<style lang="scss" scoped>


.portfolio #portfolio-filters {
  padding: 0;
  margin: 0 auto 25px auto;
  list-style: none;
  text-align: center;
  border-radius: 50px;
}

.portfolio #portfolio-filters li {
  cursor: pointer;
  display: inline-block;
  padding: 8px 16px 10px 16px;
  font-size: 14px;
  font-weight: 500;
  line-height: 1;
  color: #444444;
  margin: 0 3px 10px 3px;
  transition: all ease-in-out 0.3s;
  background: #f4f4f4;
  border-radius: 50px;
}

.portfolio #portfolio-filters li:hover,
.portfolio #portfolio-filters li.filter-active {
  color: #fff;
  background: $color-primary;
}

.portfolio #portfolio-filters li:last-child {
  margin-right: 0;
}

.portfolio .portfolio-item {
  margin-bottom: 30px;
  overflow: visible;
}

.portfolio .portfolio-item img {
  position: relative;
  top: 0;
  transition: all 0.6s cubic-bezier(0.645, 0.045, 0.355, 1);
}

.portfolio .portfolio-item .portfolio-info {
  opacity: 0;
  position: absolute;
  left: 15px;
  right: 15px;
  bottom: -50px;
  z-index: 3;
  transition: all ease-in-out 0.3s;
  background: $color-primary;
  padding: 15px 20px;
}

.portfolio .portfolio-item .portfolio-info h4 {
  font-size: 18px;
  color: #fff;
  font-weight: 600;
}

.portfolio .portfolio-item .portfolio-info p {
  color: #fff;
  font-size: 14px;
  margin-bottom: 0;
}

.portfolio .portfolio-item .portfolio-info .preview-link,
.portfolio .portfolio-item .portfolio-info .details-link {
  position: absolute;
  right: 50px;
  font-size: 24px;
  top: calc(50% - 18px);
  color: white;
  transition: ease-in-out 0.3s;
}

.portfolio .portfolio-item .portfolio-info .preview-link:hover,
.portfolio .portfolio-item .portfolio-info .details-link:hover {
  color: #33ffb4;
}

.portfolio .portfolio-item .portfolio-info .details-link {
  right: 15px;
}

.portfolio .portfolio-item:hover img {
  top: -30px;
}

.portfolio .portfolio-item:hover .portfolio-info {
  opacity: 1;
  bottom: 0;
}


.portfolio-details {
  padding-top: 40px;
}

.portfolio-details .portfolio-details-slider img {
  width: 100%;
}

.portfolio-details .portfolio-details-slider .swiper-pagination {
  margin-top: 20px;
  position: relative;
}

.portfolio-details .portfolio-details-slider .swiper-pagination .swiper-pagination-bullet {
  width: 12px;
  height: 12px;
  background-color: #fff;
  opacity: 1;
  border: 1px solid $color-primary;
}

.portfolio-details .portfolio-details-slider .swiper-pagination .swiper-pagination-bullet-active {
  background-color: $color-primary;
}

.portfolio-details .portfolio-info {
  padding: 30px;
  box-shadow: 0px 0 30px rgba(40, 40, 40, 0.08);
}

.portfolio-details .portfolio-info h3 {
  font-size: 22px;
  font-weight: 700;
  margin-bottom: 20px;
  padding-bottom: 20px;
  border-bottom: 1px solid #eee;
}

.portfolio-details .portfolio-info ul {
  list-style: none;
  padding: 0;
  font-size: 15px;
}

.portfolio-details .portfolio-info ul li+li {
  margin-top: 10px;
}

.portfolio-details .portfolio-description {
  padding-top: 30px;
}

.portfolio-details .portfolio-description h2 {
  font-size: 26px;
  font-weight: 700;
  margin-bottom: 20px;
}

.portfolio-details .portfolio-description p {
  padding: 0;
}
</style>
