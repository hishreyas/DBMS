***
Name :- Shreyas Bansode\
Class :- T.Y. BSc.- Computer Science\
Div :- A\
Roll No.:- 6\
Batch 1\
Web Assignment 4


***
# Set A
**Question A**
```php

<html>
<head>
  
<meta name="viewport" content="width=device-width, initial-scale=1.0">

	<title>Input Form</title>
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
</head>
<body>

  
    <h2>File Content and size</h2>

    <form action="setAa.php" method="POST"> File Name:

        <input type="text" name="fileName"> <br> 

        <input type="submit" value="Submit">

    </form>
    
      
  <?php
  
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
  
  function dispfilesize($filesize)
{
 
if(is_numeric($filesize))
{
 $decr = 1024; $step = 0;
$prefix =
array('Byte','KB','MB','GB','TB','PB');
while(($filesize / $decr) > 0.9)
{ $filesize = $filesize / $decr;
$step++;
 }
 return round($filesize,2).' '.$prefix[$step];
}
 else
{
return 'NaN';
}
}
  
  
  $fileName=$_POST["fileName"];
  $myfile = fopen($fileName, "r") or die("Unable to open file!");


  echo "<h1>"."File Content : </h1>".fread($myfile,filesize($fileName))."<br/>";
  echo "<h1>"."File Size:  </h1> ".dispfilesize(filesize($fileName))."<br/>";
  fclose($myfile);
  
  
}
?>
    
    
</body>
</html>
```
**Question B**
```php


<html>
<head>

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Input Form</title>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
</head>
<body>


<h2>Approve Committee</h2>

<form action="setAb.php" method="POST"> Enter Event title:

<input type="text" name="title"> <br> 

<input type="submit" value="Submit">

</form>

<?php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
  
  $title=$_POST['title'];
  $host = "host=127.0.0.1";
  $port = "port=5432";
  $dbname = "dbname = ty";
  $credentials = "user = shreyas password=hack";
  $db = pg_connect( "$host $port $dbname $credentials" );
  if(!$db) {
    echo "Error : Unable to open database\n";
  } else {
    echo "Opened database successfully\n";
  }
  $sql =" UPDATE committee set status = 'Approved' where cno in 
  (SELECT cno FROM comm_event where eno in
  (SELECT eno FROM Event where title='$title'))
  ";
  $ret = pg_query($db, $sql);
  if(!$ret) {
    echo pg_last_error($db);
    exit;
  } else {
    echo "<br>"."Record updated successfully\n";
  }
  
  $sql ="SELECT * from Committee;";
  $ret = pg_query($db, $sql);
  if(!$ret) {
    echo pg_last_error($db);
    exit;
  } 
  
  echo('<table border="1"> 
  <tr>
  <th rowspan="1">CNO</th>
  <th rowspan="1">NAME</th>
  <th rowspan="1">HEAD</th>
  <th rowspan="1">FROM</th>
  <th rowspan="1">TO</th>
  <th rowspan="1">STATUS</th>
  </tr>');
  
  while($row = pg_fetch_row($ret)) {
    
    echo"<tr>";
    echo "<td>".$row[0]."</td>";
    echo "<td>".$row[1]."</td>";
    echo "<td>".$row[2]."</td>";
    echo "<td>".$row[3]."</td>";
    echo "<td>".$row[4]."</td>";
    echo "<td>".$row[5]."</td>";
    echo "</tr>";
  }
  
  echo("</table>");
  
  
  
  
  echo "Operation done successfully\n";
  pg_close($db);
}
?>

</body>
</html>
```

#Set B
**Question A**
```php






<html>
<head>
  
<meta name="viewport" content="width=device-width, initial-scale=1.0">

	<title>Input Form</title>
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
</head>
<body>

  
    <h2>Book details</h2>

    <form action="setBa.php" method="POST"> File Name:

        <input type="text" name="fileName"> <br> 

        <input type="submit" value="Submit">

    </form>
    
      
  <?php
  
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
  
  function dispfilesize($filesize)
{
 
if(is_numeric($filesize))
{
 $decr = 1024; $step = 0;
$prefix =
array('Byte','KB','MB','GB','TB','PB');
while(($filesize / $decr) > 0.9)
{ $filesize = $filesize / $decr;
$step++;
 }
 return round($filesize,2).' '.$prefix[$step];
}
 else
{
return 'NaN';
}
}
  
  
  $fileName=$_POST["fileName"];
  
  echo('<table border="1"> 
  <tr>
  <th rowspan="1">Item code</th>
	<th rowspan="1">Item name</th>
	<th rowspan="1">Unit sold</th>
	<th rowspan="1">Rate</th>
  </tr>');
  
  if ($file = fopen($fileName, "r")) {
    while(!feof($file)) {
        $line = fgets($file);
        
        $fileLine=explode(" ",$line);
        echo"<tr>";
        echo "<td>".$fileLine[0]."</td>";
        echo "<td>".$fileLine[1]."</td>";
        echo "<td>".$fileLine[2]."</td>";
        echo "<td>".$fileLine[3]."</td>";
        echo "</tr>";
        # do same stuff with the $line
    }
    fclose($file);
    
    echo("</table>");
}
  
}
?>
    
    
</body>
</html>
```
**Question B**
```php


<html>
<head>
  
<meta name="viewport" content="width=device-width, initial-scale=1.0">

	<title>Input Form</title>
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
</head>
<body>

  
    <h2>Competition Details</h2>

    <form action="setBb.php" method="POST"> Enter Competition name:

        <input type="text" name="cname"> <br> 

        <input type="submit" value="Submit">

    </form>
  
<?php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {

$cName=$_POST['cname'];
 $host = "host=127.0.0.1";
 $port = "port=5432";
 $dbname = "dbname = ty";
 $credentials = "user = shreyas password=hack";
 $db = pg_connect( "$host $port $dbname $credentials" );
 if(!$db) {
 echo "Error : Unable to open database\n";
 } else {
 echo "Opened database successfully\n";
 }
 
 $sql ="
 select Student.sid,Student.name,Student.class, Competition.c_name,stu_comp.rank,stu_comp.year
 from Student,Competition,stu_comp where Student.sid=stu_comp.sid and 
 Competition.c_no=stu_comp.c_no and Competition.c_name='$cName' 
 and stu_comp.rank=1;
 ";
 $ret = pg_query($db, $sql);
 if(!$ret) {
 echo pg_last_error($db);
 exit;
 } 
 
 echo('<table border="1"> 
  <tr>
  <th rowspan="1">SID</th>
	<th rowspan="1">NAME</th>
	<th rowspan="1">CLASS</th>
	<th rowspan="1">Competition</th>
	<th rowspan="1">Rank</th>
	<th rowspan="1">Year</th>
  </tr>');
  
while($row = pg_fetch_row($ret)) {
   
   echo"<tr>";
        echo "<td>".$row[0]."</td>";
        echo "<td>".$row[1]."</td>";
        echo "<td>".$row[2]."</td>";
        echo "<td>".$row[3]."</td>";
        echo "<td>".$row[4]."</td>";
        echo "<td>".$row[5]."</td>";
        echo "</tr>";
 }
    
    echo("</table>");
 
 

 echo "Operation done successfully\n";
 pg_close($db);
}
?>

</body>
</html>

```
