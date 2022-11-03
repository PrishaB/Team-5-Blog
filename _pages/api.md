---
layout: default
title: Mental Health News Articles 
permalink: /api/
---

<h1>Copy and Paste the URLs into a new tab to view the articles.</h1>
<!-- HTML table fragment for page -->
<table>
  <thead>
  <tr>
    <th>Title</th>
    <th>url</th>
  </tr>
  </thead>
  <tbody 
  id="result">
    <!-- javascript generated data -->
  </tbody>
</table>

<!-- Script is layed out in a sequence (no function) and will execute when page is loaded -->
<script>
  // prepare HTML result container for new output
  const resultContainer = document.getElementById("result");

  // prepare fetch options
const options = {
	method: 'GET',
	headers: {
		'X-RapidAPI-Key': '95798f48fcmsheb95af41fb5e7a3p1cc503jsn1c033886f550',
		'X-RapidAPI-Host': 'mental-health-info-api.p.rapidapi.com'
	}
};

fetch('https://mental-health-info-api.p.rapidapi.com/news/thetimes', options)
    // response is a RESTful "promise" on any successful fetch
    .then(response => {
      // check for response errors
      if (response.status !== 200) {
          const errorMsg = 'Database response error: ' + response.status;
          console.log(errorMsg);
          const tr = document.createElement("tr");
          const td = document.createElement("td");
          td.innerHTML = errorMsg;
          tr.appendChild(td);
          resultContainer.appendChild(tr);
          return;
      }
      // valid response will have json data
      response.json().then(data => {
          console.log(data);
          for (const row of data) {
            // tr and td build out for each row
            const tr = document.createElement("tr");
            const title = document.createElement("td");
            const url = document.createElement("td");
            // data is specific to the API
            title.innerHTML = row.title; 
            url.innerHTML = row.url; 
            // this build td's into tr
            tr.appendChild(title);
            tr.appendChild(url);
            // add HTML to container
            resultContainer.appendChild(tr);
          }
      })
  })
  // catch fetch errors (ie ACCESS to server blocked)
  .catch(err => {
    console.error(err);
    const tr = document.createElement("tr");
    const td = document.createElement("td");
    td.innerHTML = err;
    tr.appendChild(td);
    resultContainer.appendChild(tr);
  });
</script>
