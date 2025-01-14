# group tabs layout

group-tabs-layout is a state-driven UI library that integrates JSON data with Context API and dynamically renders MDX files using Next.js dynamic routing.

![group_tabs_layout_demo](https://github.com/user-attachments/assets/9e188c72-676d-4189-a638-67dd64f6ad26)

# Install

```js
pnpm add group-tabs-layout
```

# Usage

```js
"use client";

import Board from "group-tabs-layout";

const data = {
  blog: {
    selectedPageId: "page1",
    page: {
      page1: {
        id: "page1",
        groupIds: ["2a52-416f-876c-430502142051"],
        name: "page1",
      },
    },
    group: {
      "2a52-416f-876c-430502142051": {
        id: "2a52-416f-876c-430502142051",
        tabIds: ["eb7c60bd-5cf5-4872-9997-61c717b0f0c0", "5a76f275-0917-4d11-94cf-547b57be5fe6"],
        selectedTabId: "eb7c60bd-5cf5-4872-9997-61c717b0f0c0",
        size: {
          width: 400,
          height: 300,
        },
        prevSize: {
          width: 400,
          height: 300,
        },
        position: {
          x: 0,
          y: 0,
        },
        prevPosition: {
          x: 0,
          y: 0,
        },
      },
    },
    tab: {
      "eb7c60bd-5cf5-4872-9997-61c717b0f0c0": {
        id: "eb7c60bd-5cf5-4872-9997-61c717b0f0c0",
        groupId: "2a52-416f-876c-430502142051",
        name: "tab1",
        contentFile: "tab1.mdx",
      },
      "5a76f275-0917-4d11-94cf-547b57be5fe6": {
        id: "5a76f275-0917-4d11-94cf-547b57be5fe6",
        groupId: "ed3bc28c-f05c-4033-8545-3d7c16c56c07",
        name: "tab2",
        contentFile: "tab2.mdx",
      },
    },
  },
};

export default function GroupTabsLayout() {
  return (
    <Board.Root boardData={data} customConstants={{ TAB_SIZES: { WIDTH: 100, HEIGHT: 50 }, GROUP_MINIMUM_SIZE: { WIDTH: 200, HEIGHT: 300 } }}>
      <Board.Nav>
        <Board.NavList />
      </Board.Nav>
      <Board.Panel>
        <Board.GroupIndicate />
        <Board.Groups>
          <Board.Group mdxSources={mdxSources}>
            <Board.GroupHeader>
              <Board.Tab />
              <Board.TabIndicate />
            </Board.GroupHeader>
            <Board.TabContent>
              <CustomMDX />
            </Board.TabContent>
          </Board.Group>
        </Board.Groups>
      </Board.Panel>
    </Board.Root>
  );
}
```

# API

### Context API Integration

- next-group-tabs-layout package uses Context API to manage boardData prop as a state and share it globally across components.

### MDX Integration

- Add the contentFile property to tab objects in the JSON data. Each contentFile should reference an MDX file.

- Use a custom component like MdxRemote, to load and render the MDX content dynamically.

- Pass mdxContent and groupId as props to the custom MDX component.

### Board.Root

- boardData: Data to initialize the layout.

- customConstants: Object to configure constants such as tab sizes and minimum group size.

### Styling

- The package is built with Tailwind CSS. You can customize styles by overriding the provided class names.
