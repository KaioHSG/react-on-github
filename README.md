1. Install [Node.js](https://nodejs.org/en/download).

2. Run:

``` console
npx create-react-app {app-name}
```

3. Add in `package.json`:

``` json
"homepage": "https://{user-name}.github.io/{repositorie-name}"
```

E.g.: `"homepage": "kaiohsg.github.io/react-on-github"`

4. Create `.github/workflows/react-build-and-deploy.yml`:

``` yml
name: React Build and Deploy

on: 
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-22.04
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 20
      
      - name: Install Dependencies
        run: npm install
      
      - name: Build
        run: npm run build
      
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./build
```
