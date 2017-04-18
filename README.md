google-custom-form
==================

Submit to a google spreadsheet using a form of your own design.

### NOTE (8/4/2016):

I have updated this documentation to keep up with the changes Google has made to forms. The process now varies slightly from when this readme was originally published.

### INSTRUCTIONS:

* Build a google form with a question that you want to collect data for, and make sure it is public. View the form, and click on the "responses" tab. In the settings for the form (the 3 dots in the upper right) choose "select response destination" and make sure it logs to a new spreadsheet.

* View the form by clicking the "eye" icon in the upper right at the top of the page.

*  On the live form page where you can submit responses, view the source of the page, and capture the URL in the `action` attribute of the `form` tag: ex:
`https://docs.google.com/forms/d/18LD6ueL10_lLVAKpDgfmLpUBlzoRFEZSoMod57MXfH0/formResponse?hl=en_US` getting rid of everything after `formResponse?`.

* Now search the source of the page for this: 

```
<input type="hidden" name="entry.
```

Google hides the actual form input fields, so you have to search for them this way, in the source, not the web inspector (note that you cannot just do the typical "inspect" of the input element in the form, as this will not be the correct input field).

the `name` attribute, ex: `entry.1000000`. 

They do the same with the submit button, but it should be just before the closing form tag, with a name (which I think stays the same) like: `<input type="hidden" name="fbzx" value="7262277203133674908">`. That value 

* Replace the `baseURL` in the index.html file with the form action URL you copied from your Google Form.

* Replace the `submitRef` variable in the index.html file with the name and value from your submit button, ex: `&submit=7262277203133674908`.

* In our form, we are collecting names, so we've given our form an ID of `input-form` and we've given our field an ID of `input-name`. You should change this to whatever information you are collecting in your form, and change the javascript so that JQuery is grabbing the right field's value. For example, if your form has an ID of `emailForm` and your field has an ID of `input id="emailField"` your javascript should be changed to:

```
$('#emailForm').one('submit',function(){
    var inputField = encodeURIComponent($('#emailField').val());
    ...
    $('#email').addClass('active').val('Thank You!');
});
```

* Style your page how you like, put in any sort of behavior you want to have happen when someone submits an entry (we're just having the form field say 'Thank You!'), then put these files on a web server somewhere, and you should now be able to submit data to your custom form, and see it appear in your Google Spreadsheet.


### MULTIPLE QUESTIONS:

Some people have asked about incorporating multiple questions, so I've included an `index2.html` file which shows a form with two questions.

Essentially, you just need to make sure your submit URL looks like this:

```
https://docs.google.com/forms/d/[YOURFORMID]/formResponse?entry.[YOURQUESTION1IDHERE]=[YOURQUESTION1ANSWERHERE]&entry.[YOURQUESTION2IDHERE]=[YOURQUESTION2ANSWERHERE]&submit=Submit
```

where you just keep separating each question and answer with an ampersand.

entry.1=answer1&entry.2=answer2&entry3=answer3

etc.

Good luck! I have put my own sample form online [here](http://mikeheavers.com/lab/google/forms/custom-form.html) and you can view the spreadsheet with the form responses [here](https://docs.google.com/spreadsheets/d/1mzPTZC2YbQpN5IK07Fj4sENj6zajNu6TbFcHo7lD45o).


