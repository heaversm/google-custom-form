google-custom-form
==================

Submit to a google spreadsheet using a form of your own design.

###NOTE:

You can submit and view responses, but please do not edit the field values in the google spreadsheet or custom form itself! Doing so will break the example for everyone else. Someone changed the form questions and where they were sent to and so things were down for a while. Thanks!

###INSTRUCTIONS:

* Build a google form with a question that you want to collect data for, and make sure it is public.

* View the form : Form > Go To Live Form

*  View the source of this page, and capture the URL in the `action` attribute of the `form` tag: ex:
`https://docs.google.com/forms/d/18LD6ueL10_lLVAKpDgfmLpUBlzoRFEZSoMod57MXfH0/formResponse?hl=en_US` getting rid of everything after `formResponse?`.

* Now view the source of your question input field, and copy the `name` attribute, ex: `entry.1000000`. Do the same with the submit button, ex: `<input type="submit" name="submit" value="Submit">`.

* Replace the `baseURL` in the index.html file with the form action URL you copied from your Google Form.

* Replace the `submitRef` variable in the index.html file with the name and value from your submit button, ex: `&submit=Submit`.

* In our form, we are collecting names, so we've given our form an ID of `input-form` and we've given our field an ID of `input-name`. You should change this to whatever information you are collecting in your form, and change the javascript so that JQuery is grabbing the right field's value. For example, if your form has an ID of `emailForm` and your field has an ID of `input id="emailField"` your javascript should be changed to:

```
$('#emailForm').one('submit',function(){
    var inputField = encodeURIComponent($('#emailField').val());
    ...
    $('#email').addClass('active').val('Thank You!');
});
```

* Style your page how you like, put in any sort of behavior you want to have happen when someone submits an entry (we're just having the form field say 'Thank You!'), then put these files on a web server somewhere, and you should now be able to submit data to your custom form, and see it appear in your Google Spreadsheet.


###MULTIPLE QUESTIONS:

Some people have asked about incorporating multiple questions, so I've included an `index2.html` file which shows a form with two questions.

Essentially, you just need to make sure your submit URL looks like this:

```
https://docs.google.com/forms/d/[YOURFORMID]/formResponse?entry.[YOURQUESTION1IDHERE]=[YOURQUESTION1ANSWERHERE]&entry.[YOURQUESTION2IDHERE]=[YOURQUESTION2ANSWERHERE]&submit=Submit
```

where you just keep separating each question and answer with an ampersand.

entry.1=answer1&entry.2=answer2&entry3=answer3

etc.

You can view the multi-question form [here](https://docs.google.com/forms/d/1s0r2Cl5rDGMqD8u08BgUO7lvDrvO9Dr1nm9MsrWxOxQ), and the multi-question spreadsheet [here](https://docs.google.com/spreadsheets/d/1w85vK4K-aUH0zGOXAxlQ71lGA5KypdvdI0kADbB0jtc/edit#gid=567095505), as well as see a working example of a [standalone form here](http://mikeheavers.com/prototypes/google/forms/custom-form.html)


Good luck!
