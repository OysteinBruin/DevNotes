
### Getting started with Vite and React
`npm create vite@latest`


Create components folder and add a component `rafce`

### Styling
install sass as dev dependency `npm install -D sass`
create scss folder and add a file `main.scss`

```scss	
$primary-color: steelblue;

body {
  background-color: $primary-color;
}
```

Configure port for dev server in vite.config.js
Add server object:
```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  server: {
    host: '0.0.0.0',
    port: 3000,
  },
  plugins: [react()],
})
```	


### Routing

` npm install react-router-dom`

main.tsx - add BrowserRouter
```tsx
import { BrowserRouter } from 'react-router-dom';

...

  <React.StrictMode>
      <BrowserRouter>
          <App />
      </BrowserRouter>
  </React.StrictMode>,
```
https://hygraph.com/blog/routing-in-react#how-to-setup-react-router


### Typescript specifics

`npm install --save-dev @types/node`

To make e.g. `import path from "path";` in vite.config.ts compile/work


## Fetch data
`npm install axios`
#### React Query (Tanstack Query)

Install react-query and its devtools package
`npm i @tanstack/react-query`
`npm i @tanstack/react-query-devtools`

Setup:
```tsx
import { QueryClient, QueryClientProvider } from "@tanstack/react-query"
import { ReactQueryDevtools } from "@tanstack/react-query-devtools"

---

const queryClient = new QueryClient({
  defaultOptions: { queries: { staleTime: 1000 * 60 * 5 } },
})

---

  <QueryClientProvider client={queryClient}>
    <App />
    <ReactQueryDevtools initialIsOpen={false} />
  </QueryClientProvider>
```






### Build for production
run command `npm run build`
- creates a dist folder with the production build
- run production build locally with `npm run preview`


## Vite running on Asp.Net Core host
create new Asp.Net Core Web Api project
Install vite app in client folder, Create app with name e.g: 'Client' in asp.net root folder

Install package: `Miscrosoft.AspNetCore.SpaServices.Extensions`
Configure Program.cs
```cs
```


#### Resources
https://vitejs.dev/guide/
https://github.com/vitejs/awesome-vite#plugins

How to use React or Vue with Vite and Docker
- https://dev.to/ysmnikhil/how-to-build-with-react-or-vue-with-vite-and-docker-1a3l