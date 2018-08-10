# V2 Forms

Developer Ready Sync Forms

* Server Side Configurable ⚙️
* Speedy Rendering 🏃‍️
* Built in Validation ✅

## Getting Started

Sync V2 Forms are built to be backwards compatible and compatible with currently
rendering forms that are out in the wild are designed to operate the same. This
means that even existing forms can get the features of new ones as they are
added.

The most simple way to start is to let the form render itself using the
following html.

First ensure you have an HTML page / website you want to use your Sync form.

```html
<div id="revere-sync"></div>
<script async src="https://sync.revmsg.net/form/v2/<FULL FORM ID>"></script>
```

> So an example form with an ID will look like

```html
<div id="revere-sync"></div>
<script async src="https://sync.revmsg.net/form/v2/79826d9f-3930-4630-82ae-d1e25b5bfa6e"></script>
```

The form will render in the `innerHTML` of the `#revere-sync` div.

> If you would like to use multiple forms per page simply create a `div` with a `data-sync-form-id=<FULL FORM ID>` attribute. For example:

```html
<div data-sync-form-id="79826d9f-3930-4630-82ae-d1e25b5bfa6e"></div>
```

The form will render in the `innerHTML` of this `div`.

**If you do not include the first form with the `id` of `revere-sync` you will
not be able to use multiple forms. This data structure is to allow
non-conflicting renders with existing sync v2 forms that already are spread
accross the web.**

This is the basics of how to apply a sync form and use multiple per site.

## Structure of A Form

Sync V2 Forms have two structures, first is without a `data-sync-form-id` these
a fairly easy to understand.

```html
<div id="revere-sync">
   <form class="rsform" id="revere-sync-form" method="post" action="https://revere-sync-v2-stage.herokuapp.com/constituent/<access token>" name="revere-sync">
      <div class="rsform__field--required">
         <label for="name" class="rsform__field--label">Full Name *</label>
         <input id="name" class="rsform__field--text" name="name" placeholder="Full Name" required="" type="text">
      </div>
      <div class="rsform__field--required">
         <label for="email" class="rsform__field--label">Email *</label>
         <input id="email" class="rsform__field--email" name="email" placeholder="you@yourdomain.com" required="" type="email">
      </div>
      <div class="rsform__field">
         <label for="state" class="rsform__field--label">State </label>
         <select id="state" class="rsform-field--select" name="state">
            <option value="select-one">Select One</option>
            <option value="AK">AK</option>
            <!-- other states here of course-->
         </select>
      </div>
      <div class="rsform--custom_html">
         <h3>Some html here.</h3>
      </div>
      <div class="rsform--submit">
         <input class="sync-hidden-input" name="tags" value="test_1" type="hidden">
         <input class="sync-hidden-input" name="tags" value="test_2" type="hidden">
         <input id="sync-submit-button" class="rsform--submit__btn" value="Custom Submit Text" type="submit">
      </div>
   </form>
</div>
```

The important part is to notice the `id`. These are common field names that
could conflict with `ids` that already exist on the page. `email` is a common
name for an `id` so if there are errors please check to see if you already have
a conflicting `id` on the page.

The `tags` of a sync form (hidden in the `sync-hidden-input` class) are how
triggers are ran. When sync accepts these sync will run the various configured
triggers for that `tag`.

> An example with two tags active on a sync form will look like:

```html
<div id="revere-sync">
   <form class="rsform" id="revere-sync-form" method="post" action="https://revere-sync-v2-stage.herokuapp.com/constituent/<access token>" name="revere-sync">
      <div class="rsform__field--required">
         <label for="name" class="rsform__field--label">Full Name *</label>
         <input id="name" class="rsform__field--text" name="name" placeholder="Full Name" required="" type="text">
      </div>
      <div class="rsform__field--required">
         <label for="email" class="rsform__field--label">Email *</label>
         <input id="email" class="rsform__field--email" name="email" placeholder="you@yourdomain.com" required="" type="email">
      </div>
      <div class="rsform__field">
         <label for="state" class="rsform__field--label">State </label>
         <select id="state" class="rsform-field--select" name="state">
            <option value="select-one">Select One</option>
            <option value="AK">AK</option>
            <!-- other states here of course-->
         </select>
      </div>
      <div class="rsform--custom_html">
         <h3>Some html here.</h3>
      </div>
      <div class="rsform--submit">
         <input class="sync-hidden-input" name="tags" value="test_1" type="hidden">
         <input class="sync-hidden-input" name="tags" value="test_2" type="hidden">
         <input id="sync-submit-button" class="rsform--submit__btn" value="Custom Submit Text" type="submit">
      </div>
   </form>
</div>
```

## Sync V2 Forms with Data IDs

A `data-sync-form-id` is the second type of sync form. These will have the `id`
of the form at the end of each field `id` as well as on the `form` itself. **Stick to class names** or
`[data-sync-form-id="<FULL FORM ID>"] > <css selector>` in you css if you need
to style a form by it's `id`.

> Example data-sync-form with id attached

```html
<div type="revere-sync-form" data-sync-form-id="79826d9f-3930-4630-82ae-d1e25b5bfa6e">
   <form class="rsform" id="revere-sync-form-79826d9f-3930-4630-82ae-d1e25b5bfa6e" method="post" action="https://revere-sync-v2-stage.herokuapp.com/constituent/<access token>" name="revere-sync">
      <div class="rsform__field--required">
         <label for="name" class="rsform__field--label">Full Name *</label>
         <input id="name-79826d9f-3930-4630-82ae-d1e25b5bfa6e" class="rsform__field--text" name="name" placeholder="Full Name" required="" type="text">
      </div>
      <div class="rsform__field--required">
         <label for="email" class="rsform__field--label">Email *</label>
         <input id="email-79826d9f-3930-4630-82ae-d1e25b5bfa6e" class="rsform__field--email" name="email" placeholder="you@yourdomain.com" required="" type="email">
      </div>
      <div class="rsform__field">
         <label for="state" class="rsform__field--label">State </label>
         <select id="state-79826d9f-3930-4630-82ae-d1e25b5bfa6e" class="rsform-field--select" name="state">
            <option value="select-one">Select One</option>
            <option value="AK">AK</option>
            <!-- other states here of course-->
         </select>
      </div>
      <div class="rsform--custom_html">
         <h3>Some html here.</h3>
      </div>
      <div class="rsform--submit">
         <input class="sync-hidden-input" name="tags" value="test_en_page_1" type="hidden">
         <input id="sync-submit-button-79826d9f-3930-4630-82ae-d1e25b5bfa6e" class="rsform--submit__btn" value="Custom Submit Text" type="submit">
      </div>
   </form>
</div>
```

## Fancy Rendering Methods

Since Sync forms replace the `innerHTML` you can include HTML before the sync
form will load. For example a CSS loading spinner is a great thing to place into
a sync form.

> Place loading HTML inside the parent div

```html
<div id="revere-sync">
  <div class="loader">
   <!-- put your fancy css loading spinner here -->
  </div> 
</div>
```
> with an ID

```html
<div type="revere-sync-form" data-sync-form-id="a66b847e-8d4c-44c4-ad13-d7d90d1d8b63">
  <div class="loader">
    <!-- put your fancy css loading spinner here -->
  </div> 
</div>
```

Sync will then replace your HTML when the form has loaded. This keeps sync forms
compatible with most websites in terms of styles.

## Validation and Required Errors

Sync forms will always apply the same classes for errors as well as add `p` tags
into the form to alert the user something is wrong.

* Required Fields will have a `--required` class modifier on the parent of the
  `input` field as well as place a `p` tag with a class of
  `rsform__field--error` and an error message of the required field.

```html
<div class="rsform__field--required">
  <label for="email" class="rsform__field--label">Email *</label>
  <input id="email" class="rsform__field--email" name="email" placeholder="you@yourdomain.com" required="" type="email">
  <p id="email-error-missing" class="rsform__field--error">Email is required</p>
</div>
```

* Invalid information such as a bad email will have an `--invalid` as a class
  modifer when there is an invalid value as well as place `p` tag with a class
  of `rsform__field--error` and a message of the validation issue.

```html
<div class="rsform__field--invalid">
  <label for="email" class="rsform__field--label">Email *</label>
  <input id="email" class="rsform__field--email" name="email" placeholder="you@yourdomain.com" required="" type="email">
  <p id="email-error" class="rsform__field--error">Email is invalid.</p>
</div>
```

**NOTE: These modifiers will never mix, as an empty field is not invalid if it
is required.**


## Events

Each Sync V2 form can trigger events on the `document`.
Examples using jQuery v2 or v3.

## On Load
This event is fired by each form on the page after it has been written to the DOM, one for the main sync form and others with it's ids.


```html
<script>
$(document).ready(function() {
  $(document).on("sync_form_ready", function() {
    // do something here
  });
});
</script>
```

> To listen to the event of a sync form with a `data-sync-form-id`:

```html
<script>
$(document).ready(function() {
  $(document).on("sync_form_ready-<FULL FORM ID>", function() {
    // do something here
  });
});
</script>
```

> in our example form

```html
<script>
$(document).ready(function() {
  $(document).on(
    "sync_form_ready-79826d9f-3930-4630-82ae-d1e25b5bfa6e",
    function() {
      // do something here
    }
  );
});
</script>
```

## On Submit
This event fires when a user clicks the `Submit` button and data is valid in the form.

```html
<script>
$(document).ready(function() {
  $(document).on("sync_form_submit_start", function() {
    // do something here
  });
});
</script>
```

To listen to the event of a sync form with a `data-sync-form-id`:

```html
<script>
$(document).ready(function() {
  $(document).on("sync_form_submit_start-<FULL FORM ID>", function() {
    // do something here
  });
});
</script>
```

so in our example form

```html
<script>
$(document).ready(function() {
  $(document).on(
    "sync_form_submit_start-79826d9f-3930-4630-82ae-d1e25b5bfa6e",
    function() {
      // do something here
    }
  );
});
</script>
```

## On Submit Success
Fires an event when the form has been succesfully submited and data has made it to sync.

```html
<script>
$(document).ready(function() {
  $(document).on("sync_form_success", function() {
    // do something here
  });
});
</script>
```

To listen to the event of a sync form with a `data-sync-form-id`:

```html
<script>
$(document).ready(function() {
  $(document).on("sync_form_success-<FULL FORM ID>", function() {
    // do something here
  });
});
</script>
```

so in our example form

```html
<script>
$(document).ready(function() {
  $(document).on(
    "sync_form_success-79826d9f-3930-4630-82ae-d1e25b5bfa6e",
    function() {
      // do something here
    }
  );
});
</script>
```

## On Submit Fail
This event fires when there was an issue sending the data to Sync, usually from a server error.

```html
<script>
$(document).ready(function() {
  $(document).on("sync_form_submit_fail", function() {
    // do something here
  });
});
</script>
```

> To listen to the event of a sync form with a `data-sync-form-id`:

```html
<script>
$(document).ready(function() {
  $(document).on("sync_form_submit_fail-<FULL FORM ID>", function() {
    // do something here
  });
});
</script>
```

> in our example form

```html
<script>
$(document).ready(function() {
  $(document).on(
    "sync_form_submit_fail-79826d9f-3930-4630-82ae-d1e25b5bfa6e",
    function() {
      // do something here
    }
  );
});
</script>
```

***

## Google Tag Features
Sync V2 forms also push in events to the `dataLayer` for Google Tag manager to hook into. This happens at the `Submit` event after the form has been succesfully submitted.

> No data-id attribute

```html
<script>
  window.dataLayer.push({ event: "sync_form_conversion" });
</script>
```

> To listen to the event of a sync form with a `data-sync-form-id`:

```html
<script>
  window.dataLayer.push({ event: "sync_form_conversion-<FULL FORM ID>" });
</script>
```

> in our example form

```html
<script>
  window.dataLayer.push({ event: "sync_form_conversion-79826d9f-3930-4630-82ae-d1e25b5bfa6e" });
</script>
```

## Facebook Pixel Features
Sync V2 forms will always fire facebook pixel events as a standard feature. This will require the `facebook pixel id` to be configured when building the sync form. This will fire the `track` feature of the facebook sdk and contain a data value of `CompleteRegistration`. This will also use the [advanced tracking feature](https://developers.facebook.com/ads/blog/post/2016/05/31/advanced-matching-pixel/) where user information is submitted to facebook.

This requries the facebook `fpq` be present on the same site as the sync form. Sync will reinit the `fbq` sdk with it's own configured `facebook pixel id`, pass the advanced tracking data, then finally pass the `CompleteRegistration` event via:

> Facebook CompleteRegistration Event

```html
<script>
  window.fbq(
    "init",
    facebook_pixel_id, // configured facebook pixel id
    facebookData // advanced tracking data
  );

  window.fbq("track", "CompleteRegistration"); // registration event
</script>
```

With these events you should be able to take full advantage of V2 Forms! 🚀