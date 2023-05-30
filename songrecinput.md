---
layout: custom
---

<style>
  @import url('https://fonts.googleapis.com/css2?family=Dosis&display=swap');
</style>
<html>
<head>
    <title>Song Recommendor</title>
</head>
<link rel="stylesheet" href="./index.min.css" />
<body>
<h1>Song Recommendor</h1>

 

<div class="as">
        <div class="tooltip">
        <a href="songrecinput.html" class="a1">Song</a>
        <div class="bottom">Input Songs</div>
        </div>
        <div class="tooltip">
        <a href="artist.html" class="a2">Artist</a>
        <div class="bottom">Input Artists</div>
        </div>
        <div class="tooltip">
        <a href="toptracks.html" class="a4">Top Tracks</a>
        <div class="bottom">Get a list of Top Tracks daily</div>
        </div>
        <div class="tooltip">
        <a href="{{ site.baseurl }}/settings.html" class="a5">Settings</a>
        <div class="bottom">Get a list of recommendations based on your data</div>
        </div>
        <span id="loginStatus"></span>
    </div>

<p>Enter three songs you like:</p>
    <p>Song 1:</p>
    <input type="text" id="song1">
    <p>Song 2:</p>
    <input type="text" id="song2">
    <p>Song 3:</p>
    <input type="text" id="song3">
    <br>
    <br>
    <button onclick="songrec()">Recommend Songs!</button>
    <br>
    <br>
    <p>Recommended Songs:</p>
    <p id="rec"></p>
<!-- Include the JavaScript file -->

<script type="text/javascript" src="{{ site.baseurl }}/cookieCheck.js"></script>
<script>
  function songrec() {
    let expression = document.getElementById("song1").value;
    let expression2 = document.getElementById("song2").value;
    let expression3 = document.getElementById("song3").value;
    // backend not deployed yet
    const urlStart = "https://fourWsBackend.tk/api/songrec/all/";
    const url = urlStart + expression + "/" + expression2 + "/" + expression3;
    console.log(url); 
    fetch(url)
      .then(res => res.json())
      .then(data => {
        console.log(data);
        document.getElementById("rec").innerHTML = data.result; 
      })   
      }

</script>
</body>
</html>