google-custom-form
==================

Submit to a google spreadsheet using a form of your own design.

###INSTRUCTIONS:

* Build a google form with a question that you want to collect data for, and make sure it is public.

* View the form : Form > Go To Live Form

*  View the source of this page, and capture the URL in the `action` attribute of the `form` tag: ex:
`https://docs.google.com/forms/d/18LD6ueL10_lLVAKpDgfmLpUBlzoRFEZSoMod57MXfH0/formResponse?hl=en_US` getting rid of everything after `formResponse?`.

* Now view the source of your question input field, and copy the `name` attribute, ex: `entry.1000000`. Do the same with the submit button, ex: `<input type="submit" name="submit" value="Submit">`.

* Make sure references to '#input-form' are changed to match the ID of your form. For example, if your form has an ID of `emailForm` your javascript should be changed to:

```
$('#emailForm').one('submit',function(){
  var submitURL = ($('#emailForm').attr('action') + '?' + $('#emailForm').serialize());
  $(this)[0].action = submitURL;
});
      
```

* Style your page how you like, put in any sort of behavior you want to have happen when someone submits an entry (we're just having the form field say 'Thank You!'), then put these files on a web server somewhere, and you should now be able to submit data to your custom form, and see it appear in your Google Spreadsheet.
