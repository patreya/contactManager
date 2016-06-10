# 	This is a spec + data flow for the auvenior developer task.
*	Prakash Atreya


##	FrontEnd

### UserLogin
*	Page where user can input email address.
#### HTML
*	A form for user to input email.
*	User authentication (password) not done for now.  
#### JS
*	Bind event listener onSubmit to the form
*	prevent default submit
*	Get email from the input
*	use socket.io to send email to the server. 
*	Eg socket.emit('userLogin', email)


### Dashboard 
*	Page where user can see summary of the contact list. 
#### HTML
*	Add a Link/Button to add new contact UserAddContact.
*	Create a table to show current users fullName, phone, email, EditLink
*   Might also need to create company and jobtitle as hidden field
*	Depending on the number of users, add sort, search and pagination features (Optional)
#### JS
*	socket.on('dashboard', function(data)){
	 // append to the contacts table
}


### AddContact
*	Page for user to add contact
#### HTML
*	A form with fistName,LastName,phone,email,company,jobTitle etc. 
*	Hidden element with current user email.
*	Button to Add Contact
##### JS
* 	Bind event listener to OnSubmit
*	Send the information over socket to nodejs
*	Eg socket.emit('addContact', {userEmail: userEmail, contactEmail: contactEmail ....})
*	Display the success/error messages appropriately



### EditContact
*	Page for user to edit/delete contact
#### HTML
*	A form with fistName,LastName,phone,email,company,jobTitle etc. 
*	Hidden element with current user email.
* 	Edit and Delete Button
##### JS
* 	Bind event listener to OnSubmit
*	Check Edit or Delete. If Delete as for final confirmation. 
*	Send the information over socket to nodejs
*	Eg socket.emit('editContact', {userEmail: userEmail, contactEmail: contactEmail ....})
*	Eg socket.emit('deleteContact', {userEmail: userEmail, contactEmail: contactEmail ....})
*	Display the success/error messages appropriately


### DetailContact
*	Page for user to view details for one contact.
### HTML
*	A pop up modal that shows the complete details of this particular contact


##	NodeBackend
*	Basic server setup and listening
*	Connection to MongoDB
*	Socket.io configuration 
* 	Routes configuration (/, /userLogin, /userAddContact, /userEditContact, /dashboard)

## Functions related to MongoDB
*   function to create new User (optional: this is required but not part of task) 
*	function to insert new contact (input userEmail and contact attributes)
*	function to edit one contact (input userEmail and contact attributes) 
*	function to select all contacts (given userEmail)


##	MongoDB
* 	In this particular example, it might does not make sense to store contacts in two separate documents as the only differences are two attributes (company and job-title). If there were more attributes, it would make sense to store them separately. One to be called during EditContact page another for Dashboard. 

*	Document structure of user contacts
	{id: 1, userEmail:'mainuser@gmail.com', contacts: {id:1, fullName: 'Jon Doe', phone: '123456', contactEmail:'contact1@gmail.com', company:'testcompany', jobTitle: 'developer'}}



## Router and Socket Notes

var router = express.Router();

router.get('/user/:email', function(req, res) {
	var email = req.params.email;
	// get contact list from mongoDB (dummy function below)
	var contacts = getContacts(email);
	// use socket to send back the information
	// res.send(contacts) (this is traditional method);
	// need to get socketID through connection
	io.to(socket#id).emit('dashboard', contact)
});

