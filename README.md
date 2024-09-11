#PHP NOTES

___
##Establish Connection

index.php
```php
$host = "localhost";
$user = "root";
$password = "";
$dbname = "studentdb";

//data source name 
$db = "mysql:host=$host;dbname=$dbname";

$conn = new PDO($db,$user,$password);
```

##Fetch array data
1.
```php
$statement = $conn->query("SELECT * FROM students_table;");

while($row = $statement->fetch(PDO::FETCH_ASSOC)){
    echo $row['first_name'].' '.$row['last_name'].''.'<br>';
}
```
2.
```php
$statement = $conn->query("SELECT * FROM students_table;");

while($row = $statement->fetch(PDO::FETCH_OBJ)){
    echo $row->first_name.' '.$row->last_name.''.'<br>';
}
```
3.
```php
$conn->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE,PDO::FETCH_OBJ);

$statement = $conn->query("SELECT * FROM students_table;");

while($row = $statement->fetch()){
    echo $row->first_name.' '.$row->last_name.''.'<br>';
}
```
4.
```php
$conn->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE,PDO::FETCH_OBJ);

$gender = "Male";

$sql = "SELECT * FROM students_table WHERE gender = ?";

$statement = $conn->prepare($sql);
$statement->execute([$gender]);

$users = $statement->fetchAll();

foreach ($users as $user) {
    echo $user->first_name.' '.$user->last_name.' '.$user->gender.''.'<br>';
}

```
5.
```php
$conn->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE,PDO::FETCH_OBJ);

$gender = "Male";

$sql = "SELECT * FROM students_table WHERE gender = :gender";

$statement = $conn->prepare($sql);
$statement->execute(['gender' => $gender]);

$users = $statement->fetchAll();

foreach ($users as $user) {
    echo $user->first_name.' '.$user->last_name.' '.$user->gender.''.'<br>';
}
```