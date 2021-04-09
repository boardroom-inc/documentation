# Adding Your Project

## Adding a New Project

For your project to appear on Boardroom's [governance portal](https://app.boardroom.info/), you'll first have to get in touch with our team.  Please reach out to us by email at hello@boardroom.info or message us on Discord.  

However, even before approval by Boardroom, teams can submit their information to our open source repo. 

To add a new project, follow these steps below: 

1\) Add a new object to`index.ts`in the following format: 

```text
protocol_key: {
    name: "Protocol Name",
    path: "Path used in boardroom url",
    description: "Description of protocol",
    suffix: "Token",
    folder: "Folder name to host resources",
  },
```

2\) Create a folder with the same name mentioned above in the root folder of the repo.

3\) Add logo with the file name `logo.png` in the folder with an aspect ratio of 1:1. This will display in the project switcher and various other places in the app.

4\) Add an image `header.png` which will display at the top sidebar. Ideal dimensions are 400 × 150 \(W× H\)

5\) Add a folder with the name `calls` which will contain meeting note files.

6\) Raise a pull request with the changes.

### Questions? 

Join our Discord and post in the Boardroom Support Channel - [\#❓support](https://discord.gg/CEZ8WfuK8s) 

