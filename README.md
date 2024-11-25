# nuxt-tabs-example

```md
::tab-group
---
orientation: "horizontal"
---
:::tab-item
#header
Tab One

#default
Content for Tab 1
:::

:::tab-item
---
active: true
---
#header
Tab Two

#default
Content for Tab 2
:::
::
```

## Setup

Make sure to install the dependencies:

```bash
# yarn
yarn install

# npm
npm install

# pnpm
pnpm install
```

## Development Server

Start the development server on http://localhost:3000

```bash
npm run dev
```

## Production

Build the application for production:

```bash
npm run build
```

Locally preview production build:

```bash
npm run preview
```

Check out the [deployment documentation](https://nuxt.com/docs/getting-started/deployment) for more information.
