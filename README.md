# PHP-Profile_picture_upload


<?php

    if(isset($_REQUEST['submit'])){

        $uname = $_REQUEST['username'];
        $email = $_REQUEST['email'];
        $pass = $_REQUEST['password'];
//Pict
        $profile_img = $_FILES['profile_img'];
        $img_name = $profile_img['name'];
        $img_tmp_name = $profile_img['tmp_name'];

        

        if(!empty($img_name)){

            $loc = "profile_pic/";
            if(move_uploaded_file($img_tmp_name,$loc.$img_name)){
                header("location: database_view.php");
            }


        }

        $con = mysqli_connect('localhost','root','','student');
        $query = "INSERT INTO std_info (username,email,password,profile_img) VALUES ('$uname','$email','$pass','$img_name')";

        $result = mysqli_query($con,$query);

    }
   


?>



<head>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    
    <form action="index.php" method="post" enctype="multipart/form-data">
        
        <input type="text" name="username" placeholder="Username">
        <input type="email" name="email" placeholder="Email">
        <input type="password" name="password" placeholder="Password">
        <input type="file" name="profile_img" value="upload">
        <input type="submit" name="submit">
    </form>


</body>
</html>




//...........................................


<head>
    <link rel="stylesheet" href="style.css">
</head>
<body>



<?php

        $con = mysqli_connect('localhost','root','','student');
        $query = "SELECT * FROM std_info ";

        $result = mysqli_query($con,$query);


        ?>

        <table>

        <thead>
            <tr>
                <th>Id</th>
                <th>Name</th>
                <th>Email</th>
                <th>Password</th>
                <th>Profile_img</th>
                <th>Action</th>
                
            </tr>
            
        </thead>
<?php
        while($row = mysqli_fetch_assoc($result)){

            $id = $row['id'];
            $username = $row['username'];
            $email = $row['email'];
            $password = $row['password'];
            $profile_img = $row['profile_img'];

?>
            <tbody>
            <tr>
                <td><?php echo $id;  ?></td>
                <td><?php echo $username;  ?></td>
                <td><?php echo $email;  ?></td>
                <td><?php echo $password;  ?></td>
                <td><img width="50px" src="profile_pic/<?php echo $profile_img;  ?>" alt=""></td>
                <td><a href="single_data_update.php?id=<?php echo $id;?>">Edit || <a href="delete.php?id=<?php echo $id;?>">Delete</a></td>
            </tr>
            
        </tbody>
<?php
    }
?>
 </table>
<?php
   


?>

    


</body>


