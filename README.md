<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://kit.fontawesome.com/5f597d5bfd.js" crossorigin="anonymous"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/skeleton/2.0.4/skeleton.css" integrity="sha256-ECB9bbROLGm8wOoEbHcHRxlHgzGqYpDtNTgDTyDz0wg=" crossorigin="anonymous" />
    <title>Book List</title>
    <style>
        .success, .error {
            color:white;
            padding: 5px;
            margin: 5px 0 15px 0;
        }
        .success {
            background-color: green;
        }
        .error {
            background-color: red;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Add Book</h1>
        <form id="book-form">
            <div>
                <label for="title">Title</label>
                <input type="text" id="title" class="u-full-width">
            </div>
            <div>
                <label for="title">Author</label>
                <input type="text" id="author" class="u-full-width">
            </div>
            <div>
                <label for="title">ISBN</label>
                <input type="text" id="isbn" class="u-full-width">
            </div>
            <div>
                <input type="submit" value="Submit" class="u-full-width">
            </div>
        </form>
    
        <table class="u-full-width">
            <thead>
                <tr>
                    <th>Title</th>
                    <th>Author</th>
                    <th>ISBN</th>
                    <th></th>
                </tr>
            </thead>
            <tbody id="book-list"></tbody>
        </table>
    </div>


    
    <script src="app.js">
    
    //Book Constructor number 1
function Book(title, author, isbn){
    this.title = title;
    this.author = author;
    this.isbn = isbn;
}

// Ui Constructor number 2
function UI() {}

// addBookToList number 6
UI.prototype.addBookToList = function(book){
    const list = document.getElementById('book-list');
    // create tr Element
    const row = document.createElement('tr');
    // insert cols
    row.innerHTML = `
    <td>${book.title}</td>
    <td>${book.author}</td>
    <td>${book.isbn}</td>
    <td><a href="#" class="delete">X</a></td>
    `;
    
    list.appendChild(row);
}

// Show Alert number 9
UI.prototype.showAlert = function(message, className) {
    // Create div
    const div = document.createElement('div');
    // Add classes
    div.className = `alert ${className}`;
    // Add text
    div.appendChild(document.createTextNode(message));
    // Get parent
    const container = document.querySelector('.container');

    // Get form
    const form = document.querySelector('#book-form');

    // Insert alert
    container.insertBefore(div, form);

    // Timeout after 3 sec
    setTimeout(function(){
        document.querySelector('.alert').remove();
    }, 3000);
}

// Delete Book number 10
UI.prototype.deleteBook = function(target){
    if(target.className === 'delete'){
        target.parentElement.parentElement.remove();
    }
}


// clear fields number 7b
UI.prototype.clearFields = function(){
    document.getElementById('title').value = '';
    document.getElementById('author').value = '';
    document.getElementById('isbn').value = '';
}
// Event Listeners for add book number 3
document.getElementById('book-form').addEventListener('submit', function(e){
   // Get form value
    const title = document.getElementById('title').value,
         author = document.getElementById('author').value,
         isbn = document.getElementById('isbn').value

    // instantiate book number 4
    const book = new Book(title, author, isbn);

    // instantiate UI (Adding the Books to the list) number 5
    const ui = new UI();

    // validate number 8
    if(title === "" || author === "" || isbn === "") {
        ui.showAlert('Please fill in all field', 'error');
    } else {

    // (Adding the Books to the list)
    ui.addBookToList(book);

    // show success
    ui.showAlert('Book Added!', 'success');

    // Clear fields number 7a
    ui.clearFields();
    }

    e.preventDefault();
});


// Event listener for delete number 11
document.getElementById('book-list').addEventListener('click', function(e){

    // instantiate UI
    const ui = new UI();

    // Delete Book
    ui.deleteBook(e.target);

    // Show massage
    ui.showAlert('Book Removed!', 'success');
    
    e.preventDefault();
})
    
    </script>
</body>
</html>
