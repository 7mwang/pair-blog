---
layout: page
title: Welcome to our Project
---

<style>
/* Center the title */
h1 {
  text-align: center;
  margin-top: 20px;
}

/* Center the table and add spacing between the links */
.navigation-container {
  text-align: center;
  margin-top: 40px;
}

.navigation-table {
  width: auto;
  margin: 0 auto;
  border-collapse: separate;
  border-spacing: 50px; /* Adds space between the columns */
}

.navigation-table td {
  padding: 10px;
  border: 2px solid #ddd; /* Keeps the border around the links */
  border-radius: 8px;
  transition: background-color 0.3s ease;
}

/* Add styling for the links */
.nav-link {
  font-size: 20px;
  color: #333;
  text-decoration: none;
  padding: 10px 20px;
  display: block;
  transition: color 0.3s ease, background-color 0.3s ease;
}

/* Hover effect for the links */
.nav-link:hover {
  color: #007bff;
  background-color: #f0f0f0;
}
</style>

<div class="navigation-container">
  <table class="navigation-table">
    <tr>
      <td><a class="nav-link" href="{{ site.baseurl }}/intro">Introduction</a></td>
      <td><a class="nav-link" href="{{ site.baseurl }}/jokes">Jokes</a></td>
      <td><a class="nav-link" href="{{ site.baseurl }}/tracking">Tracking</a></td>
    </tr>
  </table>
</div>











<html>
<link rel="stylesheet" href="bubble-game-style.css">
<nav class = "tabList">
<head>Bubble Popper</head>
<button onclick = "showTab1()">Bubble</button>
<button onclick = "showTab2()">Shop</button>
<button onclick = "showTab3()">Artifacts</button>
<p id = "bubbleDisplay">Bubbles</p>
</nav>
<body id = "body">
<div class = "tab1" id = "tab1">
<img src = "images/bubble.png" id = "Bubble" class = "BubbleImage" draggable="false">
</div>
<div class = "tab2" id = "tab2" style = "display:none">
<div class = "upgrade1">
    <button id = "upgrade1" onclick = "upgrade1()">Increased Bubble Production</button>
    <p class = "costDisplay" id = "bubbleCost">100 Bubbles</p>
    <br>
    <button id = "upgrade2" onclick = "upgrade2()">Bubble Blower</button>
    <p class = "costDisplay" id = "bubbleCost2">1000 Bubbles</p>
</div>
</div>
<div class="tab3" id="tab3" style="display:none">
    <button id = "artifact1" onclick = "artifact1()" title = "All Bubbles have 2x value">Golden Bubbles</button>
    <p class = "costDisplay" id = "bubbleCost">100,000 Bubbles</p>
    
</div>
</div>
</body>
</html>
<script>

// Data Saving

function saveGameData() {
    const gameData = {
        bubbleCount: bubbleCount,
        bubbleIncrement: bubbleIncrement,
        cost_1: cost_1,
        count_1: count_1,
        autoBubbleAmount: autoBubbleAmount,
        cost_2: cost_2,
        count_2: count_2,
        owned_artifact1: owned_artifact1,
    }
    localStorage.setItem('bubbleGameData', JSON.stringify(gameData))
}

// Load game data from localStorage
function loadGameData() {
    const savedData = localStorage.getItem('bubbleGameData')
    if (savedData) {
        const gameData = JSON.parse(savedData)
        bubbleCount = gameData.bubbleCount
        bubbleIncrement = gameData.bubbleIncrement
        cost_1 = gameData.cost_1
        count_1 = gameData.count_1
        autoBubbleAmount = gameData.autoBubbleAmount,
        cost_2 = gameData.cost_2,
        count_2 = gameData.count_2
        owned_artifact1 = gameData.owned_artifact1
        updateUpgrade1()
        updateUpgrade2()
        updateBubbleCount()
        if (owned_artifact1) {
            document.getElementById("artifact1").innerHTML = "Golden Bubbles 1x"
        }
    }
}

// Save data before the page is closed or reloaded
window.addEventListener("beforeunload", (event) => {
    saveGameData()
})

window.addEventListener("load", (event) => {
    loadGameData()
    updateBubbleCount()
})
// Bubble Tab
bubbleCount = 10000
bubbleIncrement = 1
bubbleList = []
Bubble.addEventListener("click", (event) => {
    var i = Math.floor(Math.random()*5) + 1
    pop = new Audio('sound/pop'+ i + ".mp3")
    pop.play()
    showParticle()
    clickBubbles()
    updateBubbleCount()
})  

function showParticle() {
    var img = document.createElement("img");
    img.src = "images/bubble.png";
    img.style.width = "20px";
    img.style.height = "20px";

    img.style.position = "absolute";
    img.randHeight = Math.floor(Math.random()*window.innerHeight+100)
    img.style.top = img.randHeight + "px"
    img.style.left = Math.floor(Math.random()*window.innerWidth-100) + "px"

    document.body.appendChild(img)

    bubbleList.push(img)
}

function bubbleRise() {
    for (let i = bubbleList.length - 1; i >= 0; i--) {
        element = bubbleList[i];
        if (element.randHeight > 0) {
            element.randHeight -= 12;
            element.style.top = element.randHeight + "px";
        } else {
            element.remove();
            bubbleList.splice(i, 1);
        }
    }
}

setInterval(bubbleRise, 16)

function clickBubbles() {
    if (owned_artifact1) {
        bubbleCount = bubbleCount + 2*bubbleIncrement
    }
    
    else {
        bubbleCount = bubbleCount + bubbleIncrement
    }
}
function updateBubbleCount() {
    document.getElementById("bubbleDisplay").innerHTML = comma(bubbleCount) + " Bubbles"
}

function comma(i) {
    return Number(i).toLocaleString()
}

// Tab Functions

function showTab1() {
    document.getElementById("bubbleDisplay").style.top = "20%"
    document.getElementById("bubbleDisplay").style.left = "50%"
    document.getElementById("tab3").style.display = "none"
    document.getElementById("tab2").style.display = "none"
    document.getElementById("tab1").style.display = "block"
}

function showTab2() {
    document.getElementById("bubbleDisplay").style.top = "6%"
    document.getElementById("bubbleDisplay").style.left = "6%"
    document.getElementById("tab3").style.display = "none"
    document.getElementById("tab2").style.display = "block"
    document.getElementById("tab1").style.display = "none"
}

function showTab3() {
    document.getElementById("bubbleDisplay").style.top = "6%"
    document.getElementById("bubbleDisplay").style.left = "6%"
    document.getElementById("tab3").style.display = "block"
    document.getElementById("tab2").style.display = "none"
    document.getElementById("tab1").style.display = "none"
}

autoBubbleAmount = 0
function autoBubbles() {
    if (owned_artifact1) {
        bubbleCount += 2*autoBubbleAmount
    }
    else {
        bubbleCount += autoBubbleAmount
    }
    updateBubbleCount()
}

setInterval(autoBubbles, 1000)


// Shop Tab

base_1 = 100
cost_1 = 100
count_1 = 0
function updateUpgrade1() {
        document.getElementById("upgrade1").innerHTML = "Increased Bubble Production +" + comma((count_1+1))     
        document.getElementById("bubbleCost").innerHTML = comma(cost_1) + " Bubbles"
}

function upgrade1() {
    if (bubbleCount > cost_1) {
        count_1++
        console.log(count_1)
        bubbleIncrement++
        bubbleCount -= cost_1
        cost_1 = Math.floor(base_1*(1+count_1)**1.1)
        updateUpgrade1()
        updateBubbleCount()
        showParticle()
    }
}

base_2 = 1000
cost_2 = 1000
count_2 = 0

function updateUpgrade2() {
        document.getElementById("upgrade2").innerHTML = "Bubble Blower +" + comma(count_2)
        document.getElementById("bubbleCost2").innerHTML = comma(cost_2) + " Bubbles"
}
function upgrade2() {
    if (bubbleCount > cost_2) {
        count_2++
        autoBubbleAmount++
        bubbleCount -= cost_2
        cost_2 = Math.floor(base_2*(1+count_2)**1.2)
        updateUpgrade2()
        updateBubbleCount()
        showParticle()
    }
}

// Artifact Tab

art_cost_1 = 100000
owned_artifact1 = false
function artifact1() {
    if (!owned_artifact1 && bubbleCount > art_cost_1) {
        owned_artifact1 = true
        bubbleCount-=art_cost_1
        document.getElementById("artifact1").innerHTML = "Golden Bubbles 1x"
    }

    else {
        window.alert("You already own this!")
    }
}

</script>