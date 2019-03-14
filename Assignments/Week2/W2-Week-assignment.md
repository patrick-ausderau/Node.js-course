# Week 1 assignment

Make an Express.js app that has following features.
  * Form to upload data and image (see image below)
  * Set the coordinates by clicking Leaflet (or other) map or get the coordinates from EXIF data from JPG (take a photo with your phone).
    * [EXIF](https://github.com/gomfunkel/node-exif)
    * Leaflet example:
    ```html
    <!-- html -->
    <div id="map" style="width: 500px; height: 400px;"></div>
    ```
    ```javascript
    // JavaScript
    const map = L.map('map').setView([51.505, -0.09], 13);
    
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);
    
    map.on('click', (evt) => {
        alert("Lat, Lon : " + evt.latlng.lat + ", " + evt.latlng.lng)
    });
    
    map.on('locationfound', (evt) => {
        map.setView(ev.latlng, 13);
    });
    
    ```
  * Upload image
    * send as [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData)
    * receive with [_multer_](https://github.com/expressjs/multer)
  * Convert image to small and medium versions
    * [_sharp_](https://github.com/lovell/sharp)
  * 1st version: Save the data from the form and image urls to data.json
     * multer and/or [_body-parser_](https://github.com/expressjs/body-parser)
     * [Node Filesystem](https://nodejs.org/dist/latest-v6.x/docs/api/fs.html) or [node-jsonfile](https://github.com/jprichardson/node-jsonfile)
  * 2nd version: Save the data from the form and image urls to database
  * Display the updated data on the frontend
    * Make a frontend of your choice: browser or mobile; HTML + CSS or hybrid or native iOS or Android

![Example form](img/form.png)
