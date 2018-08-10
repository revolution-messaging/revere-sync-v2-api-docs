# V1 Forms

This is a legacy API, please use [V2 Forms](#v2-forms) if possible.

## Getting Started

These forms consist of HTML and JavaScript components.
A sample form would start as:


```html
<div class="revmsg-wrapper"> 
 <form class="revmsg-form" method="post" action="https://sync.revmsg.net/constituent/<access token>/" name="revmsg-form">
      <div class="revmsg-failure" style="display: none;">Sorry, but we failed to add you to the list. Please try again or contact <a href="tel:+18887806763">1.888.780.6763</a></div> 
<fieldset id="signup"> 

  <div class="text">
    <label for="phone">Cell Phone Number</label>
    <input type="text" id="cellphone" name="phone" placeholder="Cell Phone Number">
  </div>
  
 </fieldset> 

    <div class="submit">
      <input type="hidden" name="triggers" value="example_trigger">
      <input class="revmsg-submit-btn" type="submit" value="submit">
    </div> 

 </form> 

    <div class="revmsg-fdbk">
        <div class="revmsg-loading" style="display: none;">...loading</div>
        <div class="revmsg-success" style="display: none;">Thanks for signing up!</div>
      </div>
     </div>
 <script src="https://sync.revmsg.net/form/<FULL FORM ID>"></script>
```

The key components here are the HTML form with a name of `triggers` that allows sync to run each service setup.
These form are generated and provided to you in general so you will not have to write this html or enter the Form ID.
If you require more customization the [constituent](#constitutent) api will be more useful.

## Redirects
Sync V1 Forms have the ability to be configured to redirect to another page after submission. 

> Ensure the `revmsgConfig` is declared before the sync javascript src tag

```html
<script>
  revmsgConfig = {
      "redirect": "https://revolutionmessaging.com"
  }
</script>
<script src="https://sync.revmsg.net/form/<FULL FORM ID>">;</script>
```

## Callbacks
Sync V1 Forms also fire a callback upon submission with data and error details if they exist.

```html
<script>
revmsgConfig = {
  callback: function(data) {
    if(data.error) {
    // there was a problem, do not fire conversion code.
    // maybe show another error state/message
    } else {
    // fire conversion pixel embed
    // show a success message
    // show "share this functionality"
    // or other "YAY!" thing here.
    }
  }
}
</script>
<script src="https://sync.revmsg.net/form/<FULL FORM ID>">;</script>
```
