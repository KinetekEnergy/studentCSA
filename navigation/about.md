---
layout: page
title: About
permalink: /about/
---

## Places I've Lived

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
        /* Ensures line breaks are respected */
    }
</style>

<div class="grid-container" id="grid_container"></div>

<script>
    var container = document.getElementById("grid_container");
    var http_source = "https://upload.wikimedia.org/wikipedia/commons/";

    // Date variables
    var birthDate = new Date("2008-01-17");
    var moveToIndianaDate = new Date("2010-01-01");
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
            if (index === 0) {  // California
                timeLived.textContent = `Lived here for:\n${calculateTimeDiff(moveToCaliforniaDate, (new Date()))}`;
            } else {  // Indiana
                timeLived.textContent = `Lived here for:\n${calculateTimeDiff(birthDate, moveToIndianaDate)}`;
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
</script>

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

content

## Image Collages

![alt text](https://github.com/user-attachments/assets/27502a63-0d74-4c24-b42f-d2ad0eca57be "Personal image collage")
