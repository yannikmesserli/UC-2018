<!-- .slide: data-background="../images/bg-1.png" -->

## Building Mobile Web Apps  

<br/>

### ArcGIS API for JavaScript

<br/>

<p>Andy Gup, ESRI Redlands</p>
<p>Lloyd Heberlie, ESRI Redlands</p>
<p>Yannik Messerli, ESRI R&amp;D Center Z&uuml;rich</p>

---

<!-- .slide: data-background="../images/bg-5.png" -->

### Topics

- 3D on Mobile Devices
- Performance
- JavaScript API Example
- Progressive Web Apps
- Demo

---

<!-- .slide: data-background="../images/bg-4.png" -->

### ArcGIS JavaScript API
#### 3D on Mobile Devices

- Works on mobile
  - Apple iPhone 8
  - Apple iPad Pro 2
  - Samsung Galaxy S8
  - Samsung Galaxy S9
  - Samsung Galaxy Tab S3
- It's as simple as opening a webpage
  - http://www.arcgis.com/home/webscene/viewer.html

---

<!-- .slide: data-background="../images/bg-2.png" -->

### ArcGIS JavaScript API
#### Performance

 - Performance can vary across
   - Hardware
   - Operating System
   - Browser Vendor
 
 - Poor performance can be avoided by
   - Keeping the number of layers limited (10 - 30)
   - Using appropriate symbols for every visualization
   - Using advantageous viewpoints
   - Throttling resource consumption
   - Turning off features

---

<!-- .slide: data-background="../images/bg-3.png" -->

### JavaScript Example
#### Change Quality and Visualizations
<div class="twos">
  <div>
    <pre style="margin-left: 100px"><code class="lang-js hljs javascript">
require([
  "esri/Map",
  "esri/layers/FeatureLayer",
  "esri/layers/SceneLayer",
  "esri/views/SceneView"
], function(
  Map,
  FeatureLayer,
  SceneLayer,
  SceneView
) {
  var view = new SceneView({
    map: new Map({
      basemap: "satellite",
      ground: "world-elevation",
      layers: [
        new FeatureLayer({ url: "//services.arcgis.com/..." }),
        new SceneLayer({ url: "//services.arcgis.com/..." })
      ]
    }),
    container: "viewDiv"
  });
});
    </code></pre>
    <br>
    <small>
      <table>
        <tr>
          <td><img style="margin: 2px; width: 30px" data-play-frame="frame-performance-view" data-play-attributes="toggleSymbol" src="./images/toggle-symbol.png"></td>
          <td style="padding: 10px">featureLayer.renderer.symbol</td>
        </tr>
        <tr>
          <td><img style="margin: 2px; width: 30px" data-play-frame="frame-performance-view" data-play-attributes="toggleShadow" src="./images/toggle-shadow.png"></td>
          <td style="padding: 10px">view.environment.lighting.directShadowsEnabled</td>
        </tr>
        <tr>
          <td><img style="margin: 2px; width: 30px" data-play-frame="frame-performance-view" data-play-attributes="toggleQuality" src="./images/toggle-quality.png"></td>
          <td style="padding: 10px">view.qualityProfile<br>view.environment.atmosphere.quality</td>
        </tr>
      </table>
    </small>
  </div>
  <div class="snippet-preview">
    <iframe id="frame-performance-view" data-src="./snippets/setup-performance-view.html"></iframe>
  </div>
</div>

---

<!-- .slide: data-background="../images/bg-2.png" -->

### Progessive Web Apps
#### Service Workers

<pre><code class="lang-js hljs javascript">
// index.html

if ('serviceWorker' in navigator) {

  navigator.serviceWorker.register('./service-worker.js', { scope: './' })
    .then(function() {

      if (navigator.serviceWorker.controller) {

        // Service Worker is active

      }
      else {

        // Service Worker is installed but inactive

      }

    })
    .catch(function(error) {

      // An error occurred during Service Worker creation

    });

}
else {

  // The current browser doesn't support service workers

}

</code></pre>


---

<!-- .slide: data-background="../images/bg-3.png" -->

### Progessive Web Apps
#### Web App Manifest

<pre><code class="lang-js hljs javascript">
// index.html

<link rel='manifest' href='./manifest.json'>


// manifest.json

{
  "short_name": "Hiking trails",
  "name": "Hiking trails Swiss National Park",

  "icons": [{
    "src": "src/img/android-icon-36x36.png",
    "sizes": "36x36",
    "type": "image/png"
  }],

  "start_url": "index.html",
  "display": "standalone",

  "background_color": "#2d2b07",
  "theme_color": "#b5e2c1"
}

</code></pre>

---


<!-- .slide: data-background="../images/bg-3.png" -->

### Demo
#### [Hiking app](https://ralucanicola.github.io/hiking-app/)

---

<!-- .slide: data-background="../images/bg-final.jpg" -->

<div style="
  margin: auto auto;
  
  width: 920px;
  height: 285px;

  background-image: url(./images/esri-science-logo-white.png);
  background-size: auto 285px;
  background-blend-mode: lighten;
  background-repeat: no-repeat;
"></div>
