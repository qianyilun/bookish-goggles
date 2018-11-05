## Introduction

In this document, it will introduce how to use PHP to have CRUD (Create, Read, Update, Delete) operations with MySQL and basic Bootstrap 4.



## Steps

1. Create `POST` Form with Name and Location input fields and Save button
2. Add `div`'s and Bootstrap classes to the form to make it look good, center the form
3. Create `process.php`, add it to Form action and include it from `index.php`
4. Create the MySQL database "crud" and table "data" with id, name and location fields
5. Connect to the database and insert the Name and Location records into the "data" table if the **Save button** has been pressed
6. Connect to the database, select the existing records and create the loop to display them above the Form in an HTML table. Add Bootstrap 4 classes to style and centre the table
7. Add Edit and Delete link buttons, press the id of the record as `GET` variable in the URL in both links
8. If the **Delete button** has been clicked, delete the record from the "data" using passed id from the `$_GET['delete']` variable value
9. Create session messages and message types for Save and Delete buttons, redirect the user back to `index.php` for both
10. Display Save and Delete messages with `$_SESSION` at the top of the page using Bootstrap 4 classes appropriate for each message type
11. If the **Edit button** has been clicked, select the existing record from the database, set `$name` and `$location` variables and display them in the Form input fields. Set the `$name` and `$location` to empty strings out the if statement
12. Set the `$update` variable to true insie the Edit button if statement. Set the `$update` variable to false out the if statement
13. Add hidden input field with the value of the record id to access it from POST
14. If the **Update button** has been clicked, update the record with new `$name` and `$location` using the value from the hidden id input field. Set the value of `$id` to 0 outside the if statement.
15. Set the `SESSION` message to updated, set the message type and redirect back to `index.php`