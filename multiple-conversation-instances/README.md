# Multiple Conversation Instances

You can embed multiple Conversations on the same page. Some features such as infinite scroll pages or Single Page Applications (SPAs) require this functionality. This approach creates a `<div>` container where the Conversation's content loads.

**Important:** The `POST_ID` and `ARTICLE_URL` parameters must match the article that the Conversation relates to. If the URL changes while a user is using an infinite scroll Conversation or swapping articles in an SPA, ensure that the Conversation's `ARTICLE_URL` matches the new URL. Using an identical `ARTICLE_URL` in two different Conversations could lead to a corruption in the system. Each Conversation should also refer to a different `POST_ID`, otherwise the same Conversation will be loaded multiple times.

## Adding an Instance

The following HTML creates a Conversation container and adds a Conversation using JavaScript. Make sure to replace `SPOT_ID`, `POST_ID`, and `ARTICLE_URL` with your own values.

```html
<div class="spotim-container"></div>
<script>
  var spotId = 'SPOT_ID';
  var postId = 'POST_ID';
  var articleUrl = 'ARTICLE_URL';
  // get reference to the container:
  var container = document.querySelector('.spotim-container');
  // create the elements and set all attributes:
  var recirculationDiv = document.createElement('div');
  recirculationDiv.setAttribute('data-spotim-module', 'recirculation');
  recirculationDiv.setAttribute('data-spot-id', spotId);
  var recirculationScript = document.createElement('script');
  recirculationScript.setAttribute('async', 'true');
  recirculationScript.setAttribute('src', 'https://recirculation.spot.im/spot/' + spotId);
  var conversationScript = document.createElement('script');
  conversationScript.setAttribute('async', 'true');
  conversationScript.setAttribute('src', 'https://launcher.spot.im/spot/' + spotId);
  conversationScript.setAttribute('data-spotim-module', 'spotim-launcher');
  conversationScript.setAttribute('data-post-url', articleUrl);
  conversationScript.setAttribute('data-post-id', postId);
  // append the elements to the container:
  container.appendChild(recirculationDiv);
  container.appendChild(recirculationScript);
  container.appendChild(conversationScript);
</script>
```

## Removing an Instance

To remove one or more Conversation instances, simply clear their containers:

```html
<script>
  var container = document.querySelector('.spotim-container');
  container.innerHTML = '';
</script>
```
