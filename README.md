# LearnFramework2
## Summary
###### SPA
###### JQuery Ajax
###### PHP OOP
###### Responsive Web Design
###### Bootstrap
###### MySQL

# LearnFramework2
## Summary
###### SPA
###### JQuery Ajax
###### PHP OOP
###### Responsive Web Design
###### Mobile First
###### Bootstrap
###### MySQL

# Architecture

Every human product has a story that run-up in front of it. That story is the architecture of that product.

# The story that run-up in front of Framework2

OOP coding is nonlinear storytelling. It is an event-driven story. Every event is a small story with actors and happenings. That small story in coding we call class.  The run-time of application is a playground for objects that have instantiated from the classes. 

A class is constructed of members and methods.
OOP is based on four pillars: Abstraction, Encapsulation, Inheritance, Polymorphism. 
Here we used two of them. Abstraction here means that we coding a class with private and public members and methods. An object has been instantiated from that class show to other objects only public members and methods. Private members and methods are unknown outside or we can say are an abstraction to outside. 
Encapsulation is like a snail. He carries everything of his own with him. An object is a capsule with all members and the methods it needs. There is no borrowing between objects.

Because of the above, I started coding CRUD for the table menu in the folder admin. It was the beginning and end of my hard coding job. After that my job was copy/paste/change/clean that code in folders root and comments. In folder root, I need only READ from copied CRUD. Super. I clear others. In folder comment, for table comments, I need all CRUD. That's all. Simple isn't it.

Here I used MVC - Model, View, the Control flow of data. JQuery Ajax splits HTML from PHP and brings data asynchrony.

One page I named template goes ahead and rests all the time in the browser. It is View. Depend on our choosing links, JQuery Ajax script call PHP object - Control - which calls connection object and model object, connect to the database, query table, and by the same path bring data back in HTML inside the template.
Because the browser contains the same page, but navigation means different peaches in that page, the browsers do not see navigation but only one page, we call application like that SPA - single page application. 


# Run it at your computer
###### You have to have XAMPP or other
###### download
###### copy to htdocs
###### copy database.sql to phpMyAdmin
###### Work!

# GitHub enough to start with

###### Open your profil
###### Download repository
###### Run app at your computer
###### Change/add code

## Commit
###### Click at LearnFramework1 in repository ivicakartelo/LearnFramework1
###### Upload files
###### Choose your files
###### Drag files here to add them to my repository
###### Commit changes
###### Commit changes

## Fork
###### Click at LearnFramework1 in repository ivicakartelo/LearnFramework1
###### Fork
###### You will have my repository as yours

# The architecture in details

Folder 'admin' contains CRUD scripting for table 'menu' organize in subfolders 'control', 'model'. Home Page index.php is View part of data flow MVC.
	admin
		control
		model
		index.php

Home Page index.php
The PHP script on the beginning is for session control:
<?php
session_start();
if (!empty($_SESSION["username"])) {  
}
else
header("Location: login/login_form.php");
Follow the variable $contain with include ("template.php") on the PHP's end. That template.php is always in browser. Because of that it is Single Page in name SPA = Single Page Application:

$content = '
    <div class="grid12">
        <h1>All menu</h1>
    </div>
        
    <div class="grid12 last">
        <table id="post" class="table">
        <thead>
        <tr>
        <th>Name</th>
        <th>Published</th>
        <th>Content</th>
        <th>Edit</th>
        <th>Delete</th>
        </tr>
        </thead>
        </table>    
    </div>
    <div class="grid12" style="padding: 20px 0 20px 0;">
        <h6>Kartedium CMS OOP</h6>
    </div>';
        include ("template.php");
?>
HTML document 'template.php' on the end has this PHP script:
<?php echo $content; ?>
It's the patch in template.php.
Index.php continues with a JQuery Ajax scripts:
'JQuery Ajax read all posts' beginns with:
$(document).ready(function()
It means that the script runs immediately after the HTML document has loaded.
 function Delete(menu_id):
It means that the script have to be colled. It is by click on button see above in the HTML:
onClick=Delete('"+data[user].menu_id+"')
The first JQuery Ajax calls URL control/select_control.php:
<?php
// include database and object files
include_once '../../model/database.php';
include_once '../model/menu.php';
 
// get database connection
$database = new Database();
$db = $database->getConnection();
 
// prepare post object
$post = new Post($db);
 
// query post
$stmt = $post->read();
$num = $stmt->rowCount();
// check if more than 0 record found
if($num>0){
 
    // posts array
    $posts_arr=array();
    $posts_arr["menu"]=array();
 
    while ($row = $stmt->fetch(PDO::FETCH_ASSOC)){
        extract($row);
        $post_item=array(
            "menu_id" => $menu_id,
            "name" => $name,
            "content" => $content,
            "published" => $published
        );
        array_push($posts_arr["menu"], $post_item);
    }
    echo json_encode($posts_arr["menu"]);
}
else{
    echo json_encode(array());
}
?>
The object $post calls its method read():
$post->read()
The path of Class Post is model/menu.php where PHP script of function read stored:
function read(){
    
        //query select all posts desc
        $query = "SELECT menu_id, name, content, published
                FROM " . $this->table_name . " 
                ORDER BY menu_id DESC";
    
        // prepare query statement
        $stmt = $this->conn->prepare($query);
    
        //execute query
        $stmt->execute();
    
        return $stmt;
    }
The function return data from the database, from the table menu to select_control.php. 
By the help of loop While and function fetch here is the array:
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)){
        extract($row);
        $post_item=array(
            "menu_id" => $menu_id,
            "name" => $name,
            "content" => $content,
            "published" => $published
        );
The array is being encoding to JSON:
echo json_encode($posts_arr["menu"]);
That JSON go to JQuery Ajax on index.php. Loop For scripts HTML table tag with rows of table menu 

for(var user in data){
                response += "<tr>"+
                "<td>"+data[user].name+"</td>"+
                "<td>"+data[user].published+"</td>"+
                "<td><div class=''>"+data[user].content+"</div></td>"

and embeds it in HTML elements named post:

$(response).appendTo($("hashpost"));

That embedded HTML is like the patch in the static template.php. All pages are the patches.

It is the architecture of the SPA. Every patch passes this path.  
