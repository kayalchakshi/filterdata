# filterdata

<html><head>
  <title>Convert JSON Data to HTML Table</title>
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
  <style>
    *{
      font-family : Cambria;
    }
    th
    {
      text-align:center;
      color:white;
      background-color:black;
      font-weight:bolder; 
      font-size : 18px;
    }
    h1{
      margin:10px 30px 60px 30px;
    }
    /* input{
      margin:0 30px 60 30px;
    } */
    td
    {
      text-align:justify;
      font-size : 16px;
      padding:20px 10px 10px 10px;
    }
    #nue{
      display:none;
    }
    button{
      margin:auto;
      display:block;
    }
  </style>
  <script>
      const mydata = 
        []
    //   list;
    //     oldlist;
    //     result =[];
    //     content
       today = new Date().toJSON().split('T')[0];
    //     startdate;
    //     enddate;
    function CreateTableFromJSON() {   
        var col = [];
            for (var i = 0; i < mydata.length; i++) {
                for (var key in mydata[i]) {
                    if (col.indexOf(key) === -1) {
                        col.push(key);
                    }
                }
            }

            // CREATE DYNAMIC TABLE.
            var table = document.createElement("table");

            // CREATE HTML TABLE HEADER ROW USING THE EXTRACTED HEADERS ABOVE.

            var tr = table.insertRow(-1);                   // TABLE ROW.

            for (var i = 0; i < col.length; i++) {
                var th = document.createElement("th");      // TABLE HEADER.
                th.innerHTML = col[i];
                tr.appendChild(th);
            }

            // ADD JSON DATA TO THE TABLE AS ROWS.
            for (var i = 0; i < mydata.length; i++) {

                tr = table.insertRow(-1);

                for (var j = 0; j < col.length; j++) {
                    var tabCell = tr.insertCell(-1);
                    tabCell.innerHTML = mydata[i][col[j]];
                }
            }

            // FINALLY ADD THE NEWLY CREATED TABLE WITH JSON DATA TO A CONTAINER.
            var divContainer = document.getElementById("showData");
            divContainer.innerHTML = "";
            divContainer.appendChild(table);
    }



    function myFunction() {
        var startdate = document.getElementById("startdate").value;
        var enddate = document.getElementById("enddate").value;
        if(this.startdate <= this.enddate){
        var std= this.startdate;
        std = std.split('-').reverse().join('-');
        var nwd = this.enddate;
        nwd = nwd.split('-').reverse().join('-');
        // document.getElementById("old").style.display = 'none';
        // document.getElementById("nue").style.display = 'block';
        
        this.list = this.mydata.filter(m => m.entryDate >= std && m.entryDate <= nwd);
        this.result = this.list;
        console.log(this.result);}else alert("enter the dates correctly");
    }

  </script>
</head>
<body>
<h1><u>List of the Data</u></h1>
<table align="center">
  <tr>
    <td>Start date - </td>
    <td><input  class="form-control" type="date" max= id="startdate"></td>
  </tr><br>
  <tr>
    <td>End date - </td>
    <td><input  class="form-control" type="date" [max]="today" id="enddate"></td>
  </tr>
  <tr>
    <td colspan="2">
      <button (click)="myFunction();" class="btn btn-default">Filter
      </button>
    </td>
  </tr>
</table>
<br><br>
<button onclick="CreateTableFromJSON()" >view JSON</button>
    <p id="showData"></p>
 <!-- <div id="old">
  <table class="table table-striped data">
    <tr>
      <th>ARTICLE NAME</th>
      <th>DOC ID</th>
      <th>DOC CONTENT</th>
      <th>ENGINE TYPE</th>
      <th>ERROR ID</th>
    </tr>
    <tr *ngFor="let d of mydata" >
      <td></td>
      <td>{{d.docID}}</td>
      <td>{{d.domContent}}</td>
      <td>{{d.errorJSON.engineType}}</td>
      <td>{{d.errorID}}</td>
    </tr>
  </table>
  </div> -->
  </body>
  </html>
