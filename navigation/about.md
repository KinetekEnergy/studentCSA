---
layout: page
title: About
permalink: /about/
comments: true
---

<style>
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
        gap: 10px;
    }

    .grid-item {
        text-align: center;
        border-radius: 5px;
    }

    .grid-item img {
        width: 100%;
        object-fit: contain;
        border-radius: 5px !important;
    }

    .grid-item p {
        margin: 5px 0;
        white-space: pre-line;
    }

    .slider {
        box-shadow: 0 10px 20px -5px rgba(0, 0, 0, 0.125);
        height: 200px;
        margin: auto;
        overflow: hidden;
        position: relative;
        border-radius: 5px;
    }

    .slider::before,
    .slider::after {
        background: linear-gradient(to right, #121212 0%, rgba(255, 255, 255, 0) 100%);
        content: "";
        height: 200px;
        position: absolute;
        width: 200px;
        z-index: 2;
    }

    .slider::after {
        right: 0;
        top: 0;
        transform: rotateZ(180deg);
    }

    .slider::before {
        left: 0;
        top: 0;
    }

    .slider .slide-track {
        display: flex;
        animation: scroll 60s linear infinite;
    }

    .slider .slide {
        flex: 0 0 auto;
        width: auto;
        height: 200px;
        padding-left: 10px;
        padding-right: 10px;
    }

    .slide img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        border-radius: 5px;
    }

    @keyframes scroll {
        0% {
            transform: translateX(0);
        }
        100% {
            transform: translateX(calc(-250px * 28));
        }
    }
</style>

## Places I've Lived

<div class="grid-container" id="grid_container"></div>

## Me

My name is Aashray Reddy, a 16 year old highschool student attending Del Norte Highschool.

My interests include:

- 💻 Computers
  - Programming
    - Python, C, Arduino, hardware design and electrical engineering
  - Cybersecurity
- 🎹 Piano
- 🏄 Surfing
  - [Torrey Pines Forecast](https://www.surfline.com/surf-report/torrey-pines-state-beach/584204204e65fad6a7709994?camId=5fc81527bceda049ecf8ac63)
  - [Torrey Pines Forecast Alternative](https://www.surf-forecast.com/breaks/Torrey-Pines-State-Beach/forecasts/latest#)
  - [Beaufort Wind Scale](https://www.spc.noaa.gov/faq/tornado/beaufort.html)
  - [Forecast Guide](https://www.lapointcamps.com/blog/how-to-read-surf-forecast/)
- 🏂 Snowboarding

## 📷 [Photography](https://www.pixelpotpourri.com/)

<div class="slider">
    <div class="slide-track" id="slide-track">
        <!-- Images will be appended here via JavaScript -->
    </div>
</div>

## Image Collages
![hing](../images/photography/fish.jpg)
![Personal image collage](https://github.com/user-attachments/assets/27502a63-0d74-4c24-b42f-d2ad0eca57be)

<script>
    var container = document.getElementById("grid_container");
    var http_source = "https://upload.wikimedia.org/wikipedia/commons/";

    // Date variables
    var birthDate = new Date("2008-01-17");
    var moveToCaliforniaDate = new Date("2015-01-01");

    // flags
    var living_in_the_world = [
        { "flag": "0/01/Flag_of_California.svg", "greeting": "Hey!", "description": "California" },
        { "flag": "a/ac/Flag_of_Indiana.svg", "greeting": "How doo!", "description": "Indiana" }
    ];

    // adjusts the grammar based on date (ex: 1 month, 2 months)
    function pluralize(value, singular, plural = null) {
        if (value === 1) {
            return `${value} ${singular}`;
        } else if (value > 1 || value === 0) {
            return `${value} ${plural || singular + 's'}`;
        }
        return '';
    }

    // find the time difference between two dates
    function calculateTimeDiff(startDate, endDate) {
        var diff = endDate - startDate;

        var years = Math.floor(diff / (1000 * 60 * 60 * 24 * 365.25));
        var months = Math.floor((diff % (1000 * 60 * 60 * 24 * 365.25)) / (1000 * 60 * 60 * 24 * 30.44));
        var days = Math.floor((diff % (1000 * 60 * 60 * 24 * 30.44)) / (1000 * 60 * 60 * 24));
        var hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
        var minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
        var seconds = Math.floor((diff % (1000 * 60)) / 1000);

        var timeString = `${pluralize(years, 'year')}\n${pluralize(months, 'month')}\n${pluralize(days, 'day')}`;

        if (hours > 0 || minutes > 0 || seconds > 0) {
            timeString += `\n${pluralize(hours, 'hour')}\n${pluralize(minutes, 'minute')}\n${pluralize(seconds, 'second')}`;
        }

        return timeString;
    }

    // update the date items in real time
    function updateGridItems() {
        container.innerHTML = ""; // clear existing content

        living_in_the_world.forEach((location, index) => {
            var gridItem = document.createElement("div");
            gridItem.className = "grid-item";

            var img = document.createElement("img");
            img.src = http_source + location.flag;
            img.alt = location.flag + " Flag";

            var description = document.createElement("p");
            description.textContent = location.description;

            var greeting = document.createElement("p");
            greeting.textContent = location.greeting;

            var timeLived = document.createElement("p");

            // calculate time lived based on the location
            currentDate = new Date();
            console.log(currentDate);
            if (index === 0) {  // California
                timeLived.textContent = `Lived here for:\n${calculateTimeDiff(moveToCaliforniaDate, currentDate)}`;
            } else {  // Indiana
                timeLived.textContent = `Lived here for:\n${calculateTimeDiff(birthDate, moveToCaliforniaDate)}`;
            }

            // put it all together
            gridItem.appendChild(img);
            gridItem.appendChild(description);
            gridItem.appendChild(greeting);
            gridItem.appendChild(timeLived);

            container.appendChild(gridItem);
        });
    }

    // initial update and set interval for real-time updates every second
    updateGridItems();
    setInterval(updateGridItems, 1000);

    // Array of image URLs
    const images = [
        "../images/photography/car.jpg",
        "../images/photography/wall.jpg",
        "../images/photography/fish.jpg",
        "../images/photography/temple.jpg",
        "../images/photography/library.jpg",
        "../images/photography/pier.jpg",
        "../images/photography/mountains.jpg",
        "../images/photography/beach.jpg",
        "../images/photography/coronado1.jpg",
        "../images/photography/blackandwhite.jpg",
        "../images/photography/sunset.jpg",
        "../images/photography/building.jpg",
        "../images/photography/coronado2.jpg",
        "../images/photography/lily.jpg",
        // Add more URLs as needed
    ];

    // Function to create image elements
    function createImage(src) {
        const img = document.createElement('img');
        img.src = src;
        img.height = 200;
        img.style.objectFit = 'cover';
        img.style.borderRadius = '5px';
        return img;
    }

    // Function to add images to the track
    function addImages() {
        const track = document.getElementById('slide-track');
        images.forEach(src => {
            const slideDiv = document.createElement('div');
            slideDiv.className = 'slide';
            slideDiv.appendChild(createImage(src));
            track.appendChild(slideDiv);
        });
    }

    // Infinite loop to keep appending images
    function loopImages() {
        addImages(); // First load
        setInterval(addImages, 100); // Re-add images
    }

    // Start appending images on page load
    window.onload = loopImages;
</script>
