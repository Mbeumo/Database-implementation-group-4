<?php
session_start();


$con = mysqli_connect("localhost" ,"root" ,"" ,"facebook");
// echo $_SESSION["result"];
$pageName;
$query;

if(isset($_POST['inner-join'])){
    $sql = "select * from user inner join post on user.id_user = post.id_user";
    $pageName =  'inner join';
}

if(isset($_POST['left-join'])){
$sql = "select * from user left join post on user.id_user = post.id_user";
$pageName =  'left join';
}

if(isset($_POST['right-join'])){
$sql = "select * from user right join post on user.id_user = post.id_user";
$pageName =  'right join';
}

if(isset($_POST['full-join'])){
$sql = "select * from user left join post on user.id_user = post.id_user union select * from user right join post on user.id_user = post.id_user";
$pageName =  'full join';


}

if(isset($_POST['cross-join'])){
$sql = "select * from user cross join post";
$pageName =  'cross join';


}


?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><?php echo $pageName; ?></title>
</head>
<style>
    td,th{
        padding:10px;
    }

    </style>
<body>
    <center><h1><?php echo $pageName;?></h1></center>

    <center>
        <table border='1' style='border-collapse: collapse'>
            <tr>
                <th>id user</th>
                <th>name</th>
                <th>email</th>
                <th>age</th>
                <th>phone</th>
                <th>id post</th>
                <th>content</th>

            </tr>
            <?php
                $query = mysqli_query($con ,$sql);

                while($data = mysqli_fetch_assoc($query)){
                    ?>
                    <tr>
                        <td><?php
                            if($data['id_user'] == null){
                                echo 'null';
                            }else{
                                echo $data['id_user'];
                            } ?></td>
                        <td><?php  
                            if($data['name'] == null){
                                echo'null';
                            }else{
                                echo $data['name'];
                            } ?></td>
                        <td><?php 
                            if($data['email'] == null){
                                echo'null';
                            }else{
                                echo $data['email'];
                            } ?></td>
                        <td><?php  
                            if($data['age'] == null){
                                echo'null';
                            }else{
                                echo $data['age'];
                            } ?></td>
                        <td><?php  
                            if($data['phone'] == null){
                                echo'null';
                            }else{
                                echo $data['phone'];
                            } ?></td>
                        <td><?php 
                             if($data['id_post'] == null){
                                echo'null';
                            }else{
                                echo $data['id_post'];
                            } ?></td>
                        <td><?php  
                        if($data['content'] == null){
                                echo'null';
                            }else{
                                echo $data['content'];
                            } ?></td>
                    </tr>

                    <?php
                }
            
            
            ?>
        </table>

    </center>
    
</body>
</html>