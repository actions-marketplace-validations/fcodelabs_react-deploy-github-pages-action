# react-deploy-github-pages-action
:octocat: GitHub Action to deploy React Apps to GitHub Pages

## Customizing

### Inputs

This action supports following inputs that can be used as `step.with` keys

| Name        | Type    | Description                     |
|-------------|---------|---------------------------------|
| `build_dir` | String | Path of output files (Required) |

### Note

This action only responsible in deploying your React application to the Github Pages. So make sure you will follow necessary steps for `Installing dependencies` and `Building your React application`

## Example usage

Create `.github/workflow/deploy.yml` with the following to build on push.

```yaml
on:
  push:
    branches:
      - main

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deploy.outputs.page_url }}
    steps:
      # Checkout project repository
      - name: Checkout
        uses: actions/checkout@v3

      # Setup Node.js environment
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16.x'

      # Install dependencies
      - name: Install dependencies
        run: yarn install --prefer-offline

      # Build Application
      - name: Build application
        run: yarn build

      # Deploy to Github Pages
      - id: deploy
        name: Deploy to Github Pages
        uses: fcodelabs/react-deploy-github-pages-action@v1.0.0
        with:
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

```

## Contributing
If you find any bugs please report an issue, so it can be fixed. If you have any suggestions that would improve us, please let us know. Feel free to contribute in any way!

**We hope this action can be useful for you in someway.**

## License
The scripts and documentation in this project are released under the [MIT License](https://github.com/fcodelabs/react-deploy-github-pages-action/blob/main/LICENSE).

## Provided by Fcode Labs
[Fcode Labs](https://fcodelabs.com) - Fastest growing Software Development company based in Sri Lanka & Singapore
