---
title: Database CRUD Operations
layout: default
description: An advanced example of do database operation asynchronously between JavaScript and Backend Database. help
image: /images/database.png

---


<html>
  <head>
    <style>
      tr.match {
        background-color: maroon;
      }
    </style>
  </head>
  <body>


<p>Enter product you want to find:</p>

<input type="text" id="userInput" onkeyup="findAllergy()" placeholder="Search for product..">

<p id="out"></p>

<script>
function findAllergy() {
  // Get the table element and search input element
var table = document.getElementById("results");
var userInput = document.getElementById("userInput");


// Listen for changes to the search input element
userInput.addEventListener("input", function() {
  // Get the value of the search input
  var searchString = userInput.value.trim();

  // Initialize array to store row numbers of matching rows
  var matchingRows = [];

  // Loop through all table rows and cells
  for (var i = 0; i < table.rows.length; i++) {
    var row = table.rows[i];
    var matchFound = false;

    for (var j = 0; j < table.rows[i].cells.length; j++) {
      // Check if the cell contains the desired string
      if (table.rows[i].cells[j].textContent.includes(searchString)) {
        // If the string is found, add the row number to the matchingRows array
        matchingRows.push(i);
        matchFound = true;
        break;
      }
    }

// new
    if (matchFound) {
      row.classList.add("match");
    } else {
      row.classList.remove("match")
    }
    }
//endnew
  

  // Display which row(s) contain the search string
  var out = document.getElementById("out");
  if (matchingRows.length > 0) {
    out.textContent = "The string '" + searchString + "' was found in row(s): " + matchingRows.join(", ");
  } else {
    out.textContent = "The string '" + searchString + "' was not found in any row.";
  }
});

}
</script>
</body>
</html>


<script>
function searchProd() {
  // Declare variables
  var input, filter, table, tr, td, i, txtValue;
  input = document.getElementById("myInput");
  filter = input.value.toUpperCase();
  table = document.getElementById("results");
  tr = table.getElementsByTagName("tr");

  // Loop through all table rows, and hide those who don't match the search query
  for (i = 0; i < tr.length; i++) {
    td = tr[i].getElementsByTagName("td")[1];
    if (td) {
      txtValue = td.textContent || td.innerText;
      if (txtValue.toUpperCase().indexOf(filter) > -1) {
        tr[i].style.display = "";
      } else {
        tr[i].style.display = "none";
      }
    }
  }
}
</script>


<p>Database API</p>

<table>
  <thead>
  <tr>
    <th>Product</th>
    <th>Ingredients</th>
  </tr>
  </thead>
  <tbody id="results">
    <!-- javascript generated data -->
  </tbody>
</table>


<script>
  // prepare HTML result container for new output
  const resultContainer = document.getElementById("results");
  // prepare URL's to allow easy switch from deployment and localhost
  //const url = "https://cskinp.duckdns.org/api/clients"
  const url = "https://cskinp.duckdns.org/api/clients"
  const create_fetch = url + '/create';
  const read_fetch = url + '/';

  // Load users on page entry
  read_clients();


  // Display User Table, data is fetched from Backend Database
  function read_clients() {
    // prepare fetch options
    const read_options = {
      method: 'GET', // *GET, POST, PUT, DELETE, etc.
      mode: 'cors', // no-cors, *cors, same-origin
      cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
      credentials: 'omit', // include, *same-origin, omit
      headers: {
        'Content-Type': 'application/json'
      },
    };

    // fetch the data from API
    fetch(read_fetch, read_options)
      // response is a RESTful "promise" on any successful fetch
      .then(response => {
        // check for response errors
        if (response.status !== 200) {
            const errorMsg = 'Database read error: ' + response.status;
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
            for (let row in data) {
              console.log(data[row]);
              add_row(data[row]);
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
  }

  function create_client(){
    //Validate Password (must be 6-20 characters in len)
    //verifyPassword("click");
    const body = {
        product: document.getElementById("product").value,
        ingredients: document.getElementById("ingredients").value,
    };
    const requestOptions = {
        method: 'POST',
        body: JSON.stringify(body),
        headers: {
            "content-type": "application/json",
            'Authorization': 'Bearer my-token',
        },
    };

    // URL for Create API
    // Fetch API call to the database to create a new user
    fetch(create_fetch, requestOptions)
      .then(response => {
        // trap error response from Web API
        if (response.status !== 200) {
          const errorMsg = 'Database create error: ' + response.status;
          console.log(errorMsg);
          const tr = document.createElement("tr");
          const td = document.createElement("td");
          td.innerHTML = errorMsg;
          tr.appendChild(td);
          resultContainer.appendChild(tr);
          return;
        }
        // response contains valid result
        response.json().then(data => {
            console.log(data);
            //add a table row for the new/created userid
            add_row(data);
        })
    })
  }

  function add_row(data) {
    const tr = document.createElement("tr");
    const product = document.createElement("td");
    const ingredients = document.createElement("td");
  

    // obtain data that is specific to the API
    product.innerHTML = data.product; 
    ingredients.innerHTML = data.ingredients; 


    // add HTML to container
    tr.appendChild(product);
    tr.appendChild(ingredients);

    resultContainer.appendChild(tr);
  }
</script>














### Serum

<html>
<body>
<form id="uinput" action="#">
  Allergy: <input type="text" name="allergy"
  id="allergy"><br>
  Product: <input type="text" name="product" id="product"><br>
  <input type=button onclick="allergyCheck()" value="Submit">
</form>
</body>



<p>Database API</p>

<table>
  <thead>
  <tr>
    <th>Product</th>
    <th>Ingredients</th>
  </tr>
  </thead>
  <tbody id="results">
    <!-- javascript generated data -->
  </tbody>
</table>


<script>
const table = document.getElementById('results');
const productIn = document.getElementById('product');
const allergyIn = document.getElementById('allergy');

function allergyCheck()
{
    var allergyl = allergyIn.value.toLowerCase();
    var productl = productIn.value.toLowerCase();
    
    for (var i = 0; i < table.rows.length; i++) {
        const row = table.rows[i];

        for (var j = 0; j < row.cells.length; j++) {
            const cell = row.cells[j];

            if (cell.innerText.toLowerCase().includes(productl)) {
                console.log(`product found in row ${i}`);
                var rowIndex = i;
                var prodrow = table.rows[rowIndex];

                for (let b = 0; b < prodrow.cells.length; b++) {
                    const prodcell = prodrow.cells[b];

                    if (prodcell.innerText.toLowerCase().includes(allergy)) {
                        console.log('this product is unsafe, return to product selection');
                        return;
                    } else {
                        console.log('this product is safe for use! enjoy!');
                        return;
                    }
                }
            } else {
                console.log('product not in our database');
            }
        }
    }
}  
            
</script>




<script>
const table = document.getElementById('results');
const productIn = document.getElementById('product');
const allergyIn = document.getElementById('allergy');

function allergyCheck()
{
    var allergyl = allergyIn.value.toLowerCase();
    var productl = productIn.value.toLowerCase();
    
    for (var i = 0; i < table.rows.length; i++) {
        const row = table.rows[i];

        for (var j = 0; j < row.cells.length; j++) {
            const cell = row.cells[j];

            if (cell.innerText.toLowerCase().includes(productl)) {
                console.log(`product found in row ${i}`);
                var rowIndex = i;
                var prodrow = table.rows[rowIndex];
                var specrow = document.querySelector('#results tr:nth-child(${i})');
                var speccells = specrow.querySelectorAll("td");

                for (var k = 0; k < speccells.length; k++) {
                    const prodcell = prodrow.cells[i];

                    if (speccells[i].innerText.toLowerCase().includes(allergyl)) {
                        console.log('this product is unsafe, return to product selection');
                        return;
                    } else {
                        console.log('this product is safe for use! enjoy!');
                        return;
                    }
                }
            } else {
                console.log('product not in our database');
            }
        }
    }
}  
            
</script>


//try individual column

<script>
const table = document.getElementById('results');
const productIn = document.getElementById('product');
const allergyIn = document.getElementById('allergy');

function allergyCheck() {
    var allergyl = allergyIn.value.toLowerCase();
    var productl = productIn.value.toLowerCase();
    
    for (var i = 0; i < table.rows.length; i++) {
        const row = table.rows[i];

        for (var j = 0; j < row.cells.length; j++) {
            const cell = row.cells[j];

            if (cell.innerText.toLowerCase().includes(productl)) {
                console.log(`product found in row ${i}`);
                var rowIndex = i;
                var prodrow = table.rows[rowIndex];
                var specrow = document.querySelector(`#results tr:nth-child(${i+1})`);
                var speccells = specrow.querySelectorAll("td");

                for (var k = 0; k < speccells.length; k++) {
                    const prodcell = prodrow.cells[k];
//it is currently checking the wrong column
                    console.log(speccells[k].innerText.toLowerCase());
                    console.log(allergyl);
//how to make it check the right colum (k===1 not working)
                    if (speccells[k].innerText.toLowerCase().includes(allergyl)) {
                        console.log('this product is unsafe, return to product selection');
                        return;
                    } else {
                        console.log('this product is safe for use! enjoy!');
                        return;
                    }
                }
            } else {
                console.log('product not in our database');
            }
        }
    }
}
            
</script>



//diff column try
<script>
const table = document.getElementById('results');
const productIn = document.getElementById('product');
const allergyIn = document.getElementById('allergy');

function allergyCheck() {
    var allergyl = allergyIn.value.toLowerCase();
    var productl = productIn.value.toLowerCase();
    
    for (var i = 0; i < table.rows.length; i++) {
        const row = table.rows[i];

        for (var j = 0; j < row.cells.length; j++) {
            const cell = row.cells[j];

            if (cell.innerText.toLowerCase().includes(productl)) {
                console.log(`product found in row ${i}`);
                var specrow = document.querySelector(`#results tr:nth-child(${i})`);
                var speccell = specrow.cell[1]
//it is currently checking the wrong column
                console.log(speccell.innerText.toLowerCase());
                console.log(allergyl);
//how to make it check the right colum (k===1 not working)
                if (speccell.innerText.toLowerCase().includes(allergyl)) {
                    console.log('this product is unsafe, return to product selection');
                    return;
                } else {
                    console.log('this product is safe for use! enjoy!');
                    return;
                }
            } else {
                console.log('product not in our database');
            }
        }
    }
}

            
</script>



//this works

<script>
const table = document.getElementById('results');
const productIn = document.getElementById('product');
const allergyIn = document.getElementById('allergy');

function allergyCheck() {
    var allergyl = allergyIn.value.toLowerCase();
    var productl = productIn.value.toLowerCase();
    
    for (var i = 0; i < table.rows.length; i++) {
        const row = table.rows[i];

        for (var j = 0; j < row.cells.length; j++) {
            const cell = row.cells[j];

            if (cell.innerText.toLowerCase().includes(productl)) {
                console.log(`product found in row ${i}`);
                var rowIndex = i;
                var prodrow = table.rows[rowIndex];
                var specrow = document.querySelector(`#results tr:nth-child(${i+1})`);
                var speccells = specrow.querySelectorAll("td");

                for (var k = 1; k < speccells.length; k++) {
                    const prodcell = prodrow.cells[k];
//it is currently checking the wrong column
                    console.log(speccells[k].innerText.toLowerCase());
                    console.log(allergyl);
//how to make it check the right colum (k===1 not working)
                    if (speccells[k].innerText.toLowerCase().includes(allergyl)) {
                        console.log('this product is unsafe, return to product selection');
                        return;
                    } else {
                        console.log('this product is safe for use! enjoy!');
                        return;
                    }
                }
            } else {
                console.log('product not in our database');
            }
        }
    }
}
            
</script>
