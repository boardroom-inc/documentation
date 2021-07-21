# 1. Add Protocol Information

All project addition and edits occur on the public [Project Information repository on Github](https://github.com/boardroom-inc/protocol-Info), where all information seen in the Boardroom governance portal is uploaded, stored, and maintained. These docs will walk you through how to add the necessary project information to this repository in a few simple steps, to get your project added to the Boardroom Portal frontend.

## Add a new project

Fork the [protocol-info repo](https://github.com/boardroom-inc/protocol-Info) to your GitHub account, then clone your forked repo:

```bash
$ git@github.com:your-github-account/protocol-Info.git
```

Create a working branch:

```bash
$ git checkout -b your-project-name
```

Copy the `protocols/__example` folder to a new folder under `protocols`:

```bash
$ cp -r protocols/__example protocols/your-project-name
```

## Update project

Within your new protocol folder, update the info and assets for your project.

### Project metadata

Update the `index.json` file to define your project metadata.

| Property | Type | Description |
| :--- | :--- | :--- |
| `cname` | `string` | A unique identifier for the project. |
| `description` | `string` | A short blurb about the protocol. |
| `path` | `string` | The Boardroom portal slug for the protocol. |
| `type` | `"snapshot" \| "compoundish"` | The governance type of the protocol. |
| `isEnabled` | `boolean` | A flag defining whether or not the protocol is enabled. |
| `discourseForum.url` | `string` | The URL to the protocol Discourse forum. |
| `discourseForum.categoryId` | `string` | The category ID of the protocol Discourse forum to be sourced. |
| `safeAddress` | `string` | The Ethereum address to the project's Parcel safe. |

### Overview

Update the `overview.md` file with a high-level description of your project and its governance process \(see [Index](https://github.com/boardroom-inc/protocol-Info/blob/main/protocols/indexCoop/overview.md) for an example\).

### Resources

Add markdown files to the `resources` folder -- these can be weekly governance call notes, development and product updates, etc. Categorize these resources into subfolders \(see [Index](https://github.com/boardroom-inc/protocol-Info/tree/main/protocols/indexCoop/resources) for an example\).

### Events

1. Add one or more new events to the `events.json` file of the protocol using the following format:
2. **title**: The title of the event - this will be shown in the month and day view.
3. **url**: A URL to link to when an event is clicked.
4. **date**: The UTC date of the event in ISO 8601 format

```javascript
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

## Open pull request

Commit your changes and push your branch to your remote repository:

```bash
$ git commit -am "add your protocol name"
$ git push origin your-project-name
```

Submit a pull request to the [protocol-info repo](https://github.com/boardroom-inc/protocol-Info). The Boardroom team will then review and merge your pull request after verifying the changes.

