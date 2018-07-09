<!-- .slide: data-background="../images/bg-1.png" -->

## Building Mobile **3D** Web Apps  

#### ArcGIS API for JavaScript

<br/>

<p>Andy Gup, ESRI Redlands</p>
<p>Lloyd Heberlie, ESRI Redlands</p>
<p>Yannik Messerli, ESRI R&amp;D Center Z&uuml;rich</p>

---

<!-- .slide: data-background="../images/bg-5.png" -->

# It's ready!

[Test it](http://www.arcgis.com/home/webscene/viewer.html)

---

<!-- .slide: data-background="../images/bg-5.png" -->

### Topics

- Performance
  - Supported devices
  - Tips for better performance
<!--     - Number of features, feature symbology
    - Rendering quality
    - Shadow & lighting -->
- Build the best mobile experience (PWAs)
  - Service workers
  - App manifest

---

<!-- .slide: data-background="../images/bg-2.png" -->

### Performance

- Performance can vary across
   - Hardware
   - Operating System
   - Browser Vendor

- And depends heavily on
   - Number of layers in your scene
   - Number of features and their symbology
   - Environement settings
   - Rendering quality


---

<!-- .slide: data-background="../images/bg-4.png" -->

### Performance

Best on our officially supported devices:
  - Apple iPhone 8
  - Apple iPad Pro 2
  - Samsung Galaxy S8
  - Samsung Galaxy S9
  - Samsung Galaxy Tab S3

---

<!-- .slide: data-background="../images/bg-3.png" -->

### Performance tips
#### Number of features and symbols

Complex visualisation will decrease performance.

<div class="twos">
  <div>
    <pre style="margin-left: 100px; font-size: 110%;"><code class="lang-js hljs javascript">
      var newSymbol = {
        type: "point-3d",
        symbolLayers: [{
          type: "object",
          width: 500,
          height: 500,
          depth: 500,
          resource: { primitive: "cube" },
          material: { color: "red" }
        }]
      };

      var renderer = featureLayer.renderer.clone();
      renderer.symbol = newSymbol;
      featureLayer.renderer = renderer;
    </code></pre>
  </div>
  <div class="snippet-preview">
    <iframe id="frame-performance-view" data-src="./snippets/setup-performance-view.html" style="transform: scale(0.33);"></iframe>
  </div>
</div>

---

<!-- .slide: data-background="../images/bg-3.png" -->

### Performance tips
#### Rendering: shadows

Shadow is costly to render.

<div class="twos">
  <div>
    <pre style="margin-left: 0px; font-size: 140%;"><code class="lang-js hljs javascript" style="margin-left: -50px; padding-right: 50px;">
      view.environment
       .lighting.directShadowsEnabled = false;
    </code></pre>
  </div>
  <div class="snippet-preview">
    <iframe id="frame-performance-view" data-src="./snippets/setup-performance-view.html" style="transform: scale(0.33);"></iframe>
  </div>
</div>

---

<!-- .slide: data-background="../images/bg-3.png" -->

### Performance tips
#### Rendering quality

High rendering settings decrease performance.

<div class="twos">
  <div>
    <pre style="font-size: 140%;"><code class="lang-js hljs javascript" style="margin-left: -50px; padding-right: 50px;">
      view.environment.atmosphere.quality = "low";
      view.qualityProfile = "low";
    </code></pre>
  </div>
  <div class="snippet-preview">
    <iframe id="frame-performance-view" data-src="./snippets/setup-performance-view.html" style="transform: scale(0.33);"></iframe>
  </div>
</div>

---

<!-- .slide: data-background="../images/bg-5.png" -->

## Progressive web app

<div style="max-width: 900px; font-weight: lighter; margin: auto; padding: 30px; background: rgba(0,0,0,0.5)">A progressive web app uses standard web technology to handle vast variety of client's browsers, interruption of connection, fast user interraction to give the best mobile experience.
</div>

[Google documentation](https://developers.google.com/web/progressive-web-apps/)


---

<!-- .slide: data-background="../images/bg-2.png" -->

### Service Workers
#### Definition

<div style="max-width: 900px; font-weight: lighter; margin: auto; padding: 30px; background: rgba(0,0,0,0.5)">Service workers are Javascript scripts run by modern browsers to handle slow or intermittent network connectivity. They sit between your applications, the browser, and the network and take appropriate actions based on whether the network is available or the resource is cached.</div>

[Mozilla documentation](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)

---

<!-- .slide: data-background="../images/bg-2.png" -->

### Service Workers

<div class="twos">
  <div>
    <pre style="font-size: 90%;"><code class="lang-js hljs javascript">
    // service-worker.js

    self.addEventListener('install', event => {
      event.waitUntil(
        caches.open("your_cache")
          .then((cache) => { 
            // Cache the files you need offline
          }));
      );
    });

    self.addEventListener('fetch', function(event) {
      event.respondWith(
        // Magic goes here
      );
    });

    </code></pre>
  </div>
  <div>
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
  </div>
</div>

---

<!-- .slide: data-background="../images/bg-3.png" -->

### Progessive Web Apps
#### Web App Manifest

<pre style="max-width: 500px; margin: auto;"><code class="lang-js hljs javascript">
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

  background-image: url(../images/esri-science-logo-white.png);
  background-size: auto 285px;
  background-blend-mode: lighten;
  background-repeat: no-repeat;
"></div>
