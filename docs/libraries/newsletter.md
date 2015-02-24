#Newsletter

Binds a form to submit emails to a Mailchimp list

*Requires parsley.js for checking form input*


##Usage

HTML:

     <div class="newsletter-signup">
       <form id="newsletter-form" data-parsely-validate>
         Email: <input type="email" name="email" required></br>
         Name: <input type="name" name="name" data-pasley-minlength=3">
         <button type="submit">Sign Up</button>
       </form>
       <div id="newsletter-thanks hidden">
         Thanks for signing up to the newsletter
       </div>
       <div id="newsletter-sending hidden">
         Submitting your details...
       </div>
     </div>

JS:

     var Newsletter = require('./Newsletter');
     // instantiate the Newsletter class
     var newsletter = new Newsletter(
       $('#newsletter-form'), // jQ element of form
       $('#newsletter-thanks'), // jQ element of thanks message
       $('#newsletter-sending') // jQ element of signup
     );

