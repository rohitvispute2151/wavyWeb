<?php
    $conn= mysqli_connect('localhost','root','','crud_itv');

    if(isset($_POST['submit'])){
        $id=$_POST['id'];
        $fname=$_POST['fname'];
        $dept=$_POST['dept'];

        $sql = "insert into crudop (id,name,dept) values('$id','$fname','$dept')";

        $res = mysqli_query($conn,$sql);

        if(!$res){
            echo "<script>alert('Sorry Data not Inserted')</script>";
        }else{
           echo "<script>alert('Data Inserted Successfully')</script>";
        }
    }

?>



<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crud Operations</title>
     
    <link rel="stylesheet" href="style.css">
    
</head>
 
<body>
    <div class="container">
        <center>
            <form action="" method="POST">
                    <table border="1">
                        <tr>
                            <td>
                                ID : <input type="text" name="id" ><br>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                Name : <input type="text" name="fname" ><br>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                Dept : <input type="text" name="dept" ><br>
                            </td>
                        </tr>
                        <tr>
                            <td rowspan="1">
                                    <input type="submit" value="submit" name="submit">
                            </td>
                        </tr>
                    </table>
            </form>
        </center>

    </div>

    <div class="result">
        <center>
            <table>
                <tr>
                    <th>ID</th>
                    <th>Name</th>
                    <th>Department</th>
                    <th>operation</th>
                </tr>

                <?php
                    $conn= mysqli_connect('localhost','root','','crud_itv');

                    $sql  = "select * from crudop";
                    $res =mysqli_query($conn ,$sql);
                    while($data  = mysqli_fetch_assoc($res))
                    {
                 ?>

                        <tr>
                            <!-- here always write  what you write in  database  filed name -->
                            <td><?php  echo $data['id'];?></td>
                            <td><?php  echo $data['name'];?></td>
                            <td><?php  echo $data['dept'];?></td>
                            <td><a href="delete.php?id=<?php echo $data["id"];?>">Delete</a> | <a href="update.php?id=<?php echo $data["id"]; ?>">Update</a></td>
                        </tr>
                <?php
                    }
                ?>
                <tr>

                </tr>
                 
            </table>
        </center>
    </div>
</body>
</html>


<?php
    $conn = mysqli_connect('localhost','root','','crud_itv');
    $sql = "delete from crudop where id ='".$_GET['id']."'";

    $res  = mysqli_query($conn ,$sql);

    if($res){
        echo "Deleted " ;
        header('location:index.php');
    }
      
?>
<html>
    <body>
        <a href='index.php'>Back to Home</a>
    </body>
</html>





body {
        background-color:gray;
        color:white;
    }
    table{
      background-color:skyblue;  
      border:2px solid black; 

    }
    tr td{
        padding:10px;
    }
    .result{
        margin:20px;
        padding: 10px;
        
    }




<?php
    
    $conn= mysqli_connect('localhost','root','','crud_itv');


    if(count($_POST)>0){
       mysqli_query($conn,"update crudop set name='" . $_POST['fname'] . "',
                                             dept='" . $_POST['dept'] . "' 
                                        where id='" . $_REQUEST["id"] . "'"); 
        echo "<script>alert('Data Updated Successfully')</script>";
    }

    $sq = "select * from crudop where id ='".$_GET["id"]."'";
    $result = mysqli_query($conn,$sq);
    $data = mysqli_fetch_assoc($result);

?>


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>upadte pge</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
     <div class="container">
        
        <center>
            <form action="" method="POST">
                    <table border="1">
                        <tr>
                            <td>
                                ID : <input type="text" name="id" value= "<?php echo $data['id']?>"><br>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                Name : <input type="text" name="fname" value= "<?php echo $data['name']?>"><br>
                            </td>
                        </tr>
                        <tr>
                            <td>
                                Dept : <input type="text" name="dept" value= "<?php echo $data['dept']?>"><br>
                            </td>
                        </tr>
                        <tr>
                            <td rowspan="1">
                                    <input type="submit" value="submit" name="submit">
                            </td>
                        </tr>
                    </table>
            </form>
        </center>

    </div>
</body>
</html>
<html>
    <body>
        <a href='index.php'>Back to Home</a>
    </body>
</html>
