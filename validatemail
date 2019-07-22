function CustomValidation(input) {
	this.invalidities = [];
	this.validityChecks = [];

	//add reference to the input node
	this.inputNode = input;

	//trigger method to attach the listener
	this.registerListener();
}


CustomValidation.prototype = {
	addInvalidity: function(message) {
		this.invalidities.push(message);
	},
	getInvalidities: function() {
		return this.invalidities.join('. \n');
	},
	checkValidity: function(input) {
		for ( var i = 0; i < this.validityChecks.length; i++ ) {

			var isInvalid = this.validityChecks[i].isInvalid(input);
			if (isInvalid) {
				this.addInvalidity(this.validityChecks[i].invalidityMessage);
			}

			var requirementElement = this.validityChecks[i].element;

			if (requirementElement) {
				if (isInvalid) {
					requirementElement.classList.add('invalid');
					requirementElement.classList.remove('valid');
				} else {
					requirementElement.classList.remove('invalid');
					requirementElement.classList.add('valid');
				}

			} // end if requirementElement
		} // end for
	},
	checkInput: function() { // checkInput now encapsulated

		this.inputNode.CustomValidation.invalidities = [];
		this.checkValidity(this.inputNode);

		if ( this.inputNode.CustomValidation.invalidities.length === 0 && this.inputNode.value !== '' ) {
			this.inputNode.setCustomValidity('');
		} else {
			var message = this.inputNode.CustomValidation.getInvalidities();
			this.inputNode.setCustomValidity(message);
		}
	},
	registerListener: function() { //register the listener here

		var CustomValidation = this;

		this.inputNode.addEventListener('keyup', function() {
			CustomValidation.checkInput();
		});


	}

};

var usernameValidityChecks = [

	{
		isInvalid: function(input) {

			var emailaddressValue = $("#emailadd").val();
            var emailblockReg = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
			var invalidEmail = !emailblockReg.test(emailaddressValue);
            return invalidEmail ? true : false;
		},

		invalidityMessage: 'Please enter a valid email address',
		element: document.querySelector('.input-requirements li:nth-child(2)')
	},

	{
		isInvalid: function(input) {

            var emailaddressVal = $("#emailadd").val();
            var emailblockReg = /^([\w-\.]+@(?!gmail.com)(?!yahoo.com)(?!hotmail.com)(?!ymail.com)([\w-]+\.)+[\w-]{2,4})?$/;
			var illegalCharacters = !emailblockReg.test(emailaddressVal);
            return illegalCharacters ? true : false;
        },
        
		invalidityMessage: 'Please enter a non-personal email address\r',
		element: document.querySelector('.input-requirements li:nth-child(1)')
	}

];

var usernameInput = document.getElementById('emailadd');
usernameInput.CustomValidation = new CustomValidation(usernameInput);
usernameInput.CustomValidation.validityChecks = usernameValidityChecks;


var inputs = document.querySelectorAll('button:not([type="submit"])');
var submit = document.querySelector('button[type="submit"');
var form = document.getElementById('registration');

function validate() {
	for (var i = 0; i < inputs.length; i++) {
		inputs[i].CustomValidation.checkInput();
	}
}

submit.addEventListener('click', validate);
form.addEventListener('submit', validate);
