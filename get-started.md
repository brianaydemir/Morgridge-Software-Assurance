---
layout: form
title: Get Started
---
# Get Started

In order to get started, first fill out the form below to contact us and have us set up a private instance of the software just for you.   Your private instance allows you to upload you code safely in a way that only you will be able to access it.

Once you have filled out and submitted the contact form below, we will set up an instance of the software and contact you with a unique private URL that you can use to access it.  Then, you can set up an account and begin to analyse your software code.

<br />

<script>

	//
	// dialog methods
	//

	function error(message) {
		$('#error-dialog .modal-body').html(message);
		$('#error-dialog').modal();
		$('#error-dialog').draggable();
	}

	function success(message) {
		$('#success-dialog .modal-body').html(message);
		$('#success-dialog').modal();
		$('#error-dialog').draggable();
	}

	//
	// on click callback
	//

	$(document).ready(() => {
		$('#submit').click(function() {

			// collect form info
			//
			let languages = [];
			let first_name = $('.first-name input').val();
			let last_name = $('.last-name input').val();
			let affiliation = $('.affiliation input').val();
			let email = $('.email input').val();
			let message = $('.message textarea').val();
			$('.languages input:checked').each(function() {
				languages.push($(this).attr('value'));
			});

			if (!first_name) {
				error("Your first name is required.")
			} else if (!last_name) {
				error("Your last name is required.")
			} else if (!email) {
				error("Your email is required in order for us to notify you when your instance is ready.")
			} else {
				require(['{{site.baseurl}}/config.js'], (Config) => {

					// submit contact info
					//
					return $.ajax({
						url: Config.server + '/contact',
						type: 'POST',
						data: {
							first_name: first_name,
							last_name: last_name,
							affiliation: affiliation,
							email: email,
							languages: languages.join(', '),
							message: message
						},

						// callbacks
						//
						success: function() {
							success("Thank you for your submission.  You will be contacted when your software assurance instance is ready to use. ");
						},
						error: function() {
							error("Sorry, there was an error in submitting your request. ");
						}
					});
				});
			}
		});
	});
</script>
<form>
	<div class="first-name form-group">
		<label>First name</label>
		<div class="input-group">
			<input type="text" class="form-control" />
			<div class="input-group-append">
				<span class="input-group-text">
					<i class="active fa fa-question-circle" data-toggle="popover" data-placement="top" data-container="body" title="First name" data-content="This is the informal name or given name that you are called by."></i>
				</span>
			</div>
		</div>
	</div>
	<div class="last-name form-group">
		<label>Last name</label>
		<div class="input-group">
			<input type="text" class="form-control" />
			<div class="input-group-append">
				<span class="input-group-text">
					<i class="active fa fa-question-circle" data-toggle="popover" data-placement="top" data-container="body" title="Last name" data-content="This is your family name."></i>
				</span>
			</div>
		</div>
	</div>
	<div class="affiliation form-group">
		<label>Affiliation</label>
		<div class="input-group">
			<input type="text" class="form-control" />
			<div class="input-group-append">
				<span class="input-group-text">
					<i class="active fa fa-question-circle" data-toggle="popover" data-placement="top" data-container="body" title="Affiliation" data-content="This is the organization that you are affiliated with."></i>
				</span>
			</div>
		</div>
	</div>
	<div class="email form-group">
		<label>Email</label>
		<div class="input-group">
			<input type="text" class="form-control" />
			<div class="input-group-append">
				<span class="input-group-text">
					<i class="active fa fa-question-circle" data-toggle="popover" data-placement="top" data-container="body" title="Email" data-content="This is your email address so we can notify you when your instance is ready to use."></i>
				</span>
			</div>
		</div>
	</div>
	<div class="languages form-group">
		<label>Programming Languages</label>
		{% for item in site.data.languages %}
		<div class="form-check">
			<input class="form-check-input" type="checkbox" value="{{ item.name }}">
			<label class="form-check-label">{{ item.name }}</label>
		</div>
		{% endfor %}
	</div>
	<div class="message form-group">
		<label>Message</label>
		<div class="form-group">
			<textarea class="form-control" rows="6"></textarea>
		</div>
	</div>
</form>

<br />

<div class="buttons">
	<button id="submit" class="btn btn-primary btn-lg"><i class="fa fa-envelope"></i>Submit</button>
</div>

<!-- Modals -->
<div class="modal fade" id="error-dialog" tabindex="-1" role="dialog" aria-hidden="true">
	<div class="modal-dialog" role="document">
		<div class="modal-content">
			<div class="modal-header">
				<h3 class="modal-title">Form Error</h3>
				<button type="button" class="close" data-dismiss="modal" aria-label="Close">
					<span aria-hidden="true">&times;</span>
				</button>
			</div>
			<div class="modal-body">
			</div>
			<div class="modal-footer">
				<button type="button" class="btn btn-primary" data-dismiss="modal">OK</button>
			</div>
		</div>
	</div>
</div>

<div class="modal fade" id="success-dialog" tabindex="-1" role="dialog" aria-hidden="true">
	<div class="modal-dialog" role="document">
		<div class="modal-content">
			<div class="modal-header">
				<h5 class="modal-title">Request Sent</h5>
				<button type="button" class="close" data-dismiss="modal" aria-label="Close">
					<span aria-hidden="true">&times;</span>
				</button>
			</div>
			<div class="modal-body">
			</div>
			<div class="modal-footer">
				<button type="button" class="btn btn-primary" data-dismiss="modal">OK</button>
			</div>
		</div>
	</div>
</div>
