<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Responsive Image Slider</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      background: #f4f4f9;
    }

    .slider-container {
      position: relative;
      width: 80%;
      max-width: 800px;
      overflow: hidden;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    }

    .slider {
      display: flex;
      transition: transform 0.5s ease-in-out;
    }

    .slide {
      min-width: 100%;
      position: relative;
    }

    .slide img {
      width: 100%;
      border-radius: 10px;
    }

    .caption {
      position: absolute;
      bottom: 20px;
      left: 20px;
      background: rgba(0, 0, 0, 0.5);
      color: #fff;
      padding: 10px;
      border-radius: 5px;
      font-size: 16px;
    }

    .nav {
      position: absolute;
      top: 50%;
      width: 100%;
      display: flex;
      justify-content: space-between;
      transform: translateY(-50%);
    }

    .nav button {
      background: rgba(0, 0, 0, 0.5);
      color: #fff;
      border: none;
      padding: 10px;
      cursor: pointer;
      border-radius: 50%;
    }

    .nav button:hover {
      background: rgba(0, 0, 0, 0.8);
    }

    .thumbnails {
      display: flex;
      justify-content: center;
      margin-top: 10px;
    }

    .thumbnail {
      width: 60px;
      height: 40px;
      margin: 0 5px;
      cursor: pointer;
      opacity: 0.7;
    }

    .thumbnail img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      border-radius: 5px;
    }

    .thumbnail.active {
      opacity: 1;
      border: 2px solid #007bff;
    }

    @media (max-width: 768px) {
      .caption {
        font-size: 14px;
      }

      .thumbnail {
        width: 50px;
        height: 30px;
      }
    }
  </style>
</head>
<body>
  <div class="slider-container">
    <div class="slider">
      <div class="slide">
        <img src="https://via.placeholder.com/800x400?text=Image+1" alt="Image 1">
        <div class="caption">Caption for Image 1</div>
      </div>
      <div class="slide">
        <img src="https://via.placeholder.com/800x400?text=Image+2" alt="Image 2">
        <div class="caption">Caption for Image 2</div>
      </div>
      <div class="slide">
        <img src="https://via.placeholder.com/800x400?text=Image+3" alt="Image 3">
        <div class="caption">Caption for Image 3</div>
      </div>
    </div>
    <div class="nav">
      <button id="prev">❮</button>
      <button id="next">❯</button>
    </div>
    <div class="thumbnails">
      <div class="thumbnail" data-index="0">
        <img src="https://via.placeholder.com/800x400?text=Image+1" alt="Thumbnail 1">
      </div>
      <div class="thumbnail" data-index="1">
        <img src="https://via.placeholder.com/800x400?text=Image+2" alt="Thumbnail 2">
      </div>
      <div class="thumbnail" data-index="2">
        <img src="https://via.placeholder.com/800x400?text=Image+3" alt="Thumbnail 3">
      </div>
    </div>
  </div>

  <script>
    const slider = document.querySelector('.slider');
    const slides = document.querySelectorAll('.slide');
    const thumbnails = document.querySelectorAll('.thumbnail');
    const prevBtn = document.getElementById('prev');
    const nextBtn = document.getElementById('next');
    let currentIndex = 0;
    let autoSlideInterval;

    function updateSlider() {
      slider.style.transform = translateX(-${currentIndex * 100}%);
      thumbnails.forEach((thumbnail, index) => {
        thumbnail.classList.toggle('active', index === currentIndex);
      });
    }

    function nextSlide() {
      currentIndex = (currentIndex + 1) % slides.length;
      updateSlider();
    }

    function prevSlide() {
      currentIndex = (currentIndex - 1 + slides.length) % slides.length;
      updateSlider();
    }

    function autoSlide() {
      autoSlideInterval = setInterval(nextSlide, 3000);
    }

    thumbnails.forEach((thumbnail) => {
      thumbnail.addEventListener('click', () => {
        currentIndex = parseInt(thumbnail.dataset.index);
        updateSlider();
        clearInterval(autoSlideInterval);
        autoSlide();
      });
    });

    prevBtn.addEventListener('click', () => {
      prevSlide();
      clearInterval(autoSlideInterval);
      autoSlide();
    });

    nextBtn.addEventListener('click', () => {
      nextSlide();
      clearInterval(autoSlideInterval);
      autoSlide();
    });

    autoSlide();
  </script>
</body>
</html>
