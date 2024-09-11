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
      <td><a class="nav-link" href="{{ site.baseurl }}/github/pages/intro">Introduction</a></td>
      <td><a class="nav-link" href="{{ site.baseurl }}/github/pages/jokes">Jokes</a></td>
      <td><a class="nav-link" href="{{ site.baseurl }}/github/pages/tracking">Tracking</a></td>
    </tr>
  </table>
</div>
