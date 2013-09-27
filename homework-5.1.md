## Homework 5.1: Starting to understand more complex French

* Login to Github and approve my pull request to get the file `homework-5.1.md` in your `assignments` repository.
* Log into Cloud9 and use `git pull` to get the file into your workspace.
 
* Find [the Wordpress project on Github][wordpress], fork it into your own account, and clone it into a Cloud9 workspace.
* Open your Wordpress workspace and find a file that has some branching _if-then-else_ logic; look for some juicy conditionals and guard clauses.
* Copy-paste your examples into `homework-5.1.md` (this file) and attempt to identify the conditions with comments like so:
> USERNAME/Wordpress/path/to/file.php:00
> ```php
>   if ( $mom_says == 'yes' ) // if mom says yes
> ```

* Save your file locally, add and commit it with git, and push your changes to your Github account.
* **Bonus points**: open a pull request back to the original repo with your work to date.

[wordpress]:https://github.com/Wordpress/Wordpress/

//this code ouptputs a message "Do you like $color" and take color in the array and prints out.

<?php
$colors = array('red', 'blue', 'green', 'yellow');

foreach ($colors as $color) {
    echo "Do you like $color?\n";
}

?>

//register user 
<?php


//This function will display the registration form

function register_form(){


$date = date('D, M, Y');

echo "<form action='?act=register' method='post'>"

."Username: <input type='text' name='username' size='30'><br>"

."Password: <input type='password' name='password' size='30'><br>"

."Confirm your password: <input type='password' name='password_conf' size='30'><br>"

."Email: <input type='text' name='email' size='30'><br>"

."<input type='hidden' name='date' value='$date'>"

."<input type='submit' value='Register'>"

."</form>";


}


//This function will register users data

function register(){


//Connecting to database

$connect = mysql_connect("host", "username", "password");

if(!$connect){

die(mysql_error());

}


//Selecting database

$select_db = mysql_select_db("database", $connect);

if(!$select_db){

die(mysql_error());

}


//Collecting info

$username = $_REQUEST['username'];

$password = $_REQUEST['password'];

$pass_conf = $_REQUEST['password_conf'];

$email = $_REQUEST['email'];

$date = $_REQUEST['date'];


//Here we will check do we have all inputs filled


if(empty($username)){

die("Please enter your username!<br>");

}


if(empty($password)){

die("Please enter your password!<br>");

}


if(empty($pass_conf)){

die("Please confirm your password!<br>");

}


if(empty($email)){

die("Please enter your email!");

}


//Let's check if this username is already in use


$user_check = mysql_query("SELECT username FROM users WHERE username='$username'");

$do_user_check = mysql_num_rows($user_check);


//Now if email is already in use


$email_check = mysql_query("SELECT email FROM users WHERE email='$email'");

$do_email_check = mysql_num_rows($email_check);


//Now display errors


if($do_user_check > 0){

die("Username is already in use!<br>");

}


if($do_email_check > 0){

die("Email is already in use!");

}


//Now let's check does passwords match


if($password != $pass_conf){

die("Passwords don't match!");

}



//If everything is okay let's register this user


$insert = mysql_query("INSERT INTO users (username, password, email) VALUES ('$username', '$password', '$email')");

if(!$insert){

die("There's little problem: ".mysql_error());

}


echo $username.", you are now registered. Thank you!<br><a href=login.php>Login</a> | <a href=index.php>Index</a>";


}


switch($act){


default;

register_form();

break;


case "register";

register();

break;


}


?> 