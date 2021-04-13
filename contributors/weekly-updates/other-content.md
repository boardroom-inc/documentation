# Other Content

The Protocol Information repository allows **anyone** to make changes to the content displayed on the project-specific hubs found on the [Boardroom portal](https://app.boardroom.info). Contributors can add the following:

* **New Content Folders**
  * Will show as new tabs under the 'Resources' section
* **Markdown Files**
  * Shown in a list view inside the corresponding folder
* **Calendar** **Events**
  * These will be shown under the 'Calendar' tab

{% hint style="info" %}
Content files will be sorted by date. Add the date \(**dd-mm-yy**\) to the file name you are creating. This date will be hidden on the Boardroom portal but will sort the files by most recent.
{% endhint %}

![These tabs can be found in every project&apos;s navigation sidebar](../../.gitbook/assets/image%20%285%29.png)

## New Calendar Events

Add one or more new events to the `events.json` file of the protocol using the following format:

* **title**: The title of the event - this will be shown in the month and day view.
* **url**: A URL to link to when an event is clicked.
* **date**: The UTC date of the event in ISO 8601 format

```bash
[
  {
    "title": "This is an example event.",
    "url": "https://example.com",
    "date": "2021-01-08T00:00:00.000Z"
  },
  {
    "title": "This is another example event.",
    "url": "https://example.com",
    "date": "2021-01-10T00:00:00.000Z"
  }
]
```







