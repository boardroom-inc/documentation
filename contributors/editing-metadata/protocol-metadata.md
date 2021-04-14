---
description: >-
  You can submit a PR suggesting changes to project metadata and fields outlined
  below
---

# Protocol Metadata

## Protocol Information

Basic information of the protocol is saved in protocols object of`index.ts` file: 

```text
protocol_key: {
    name: "Protocol Name",
    path: "Path used in boardroom url",
    description: "Description of protocol",
    suffix: "Token",
    folder: "Folder name to host resources",
  },
```

Edit the corresponding value in the object and raise a new pull request for changes.

## Protocol Branding

1\) Add the unique protocol key in the object `protocolBranding` of`index.ts` if it does not exist.

```text
unique_protocol_key: {
    "--background-primary-nav": "#001529", // Background color for sidebar, header and header information in protocol pages
    "--color-text-nav": "#e7e8eb", // Color of text in sidebar, header and header information in protocol pages
    "--background-switcher-active": "#000000", // Background color of the active nav element in sidebar 
  },
```

2\) Add or edit the respective color variables and colors to the above object.

3\) Raise a PR with the changes.

4\) These changes should be reflected on the Boardroom portal a few days after the changes have been merged.

We have a code sandbox instance [https://codesandbox.io/s/boardroombranding-q3u9z](https://codesandbox.io/s/boardroombranding-q3u9z) to visualize branding changes. Change the corresponding color variable in the index.js file to have a sense of how the protocol pages will look after the updates. 

