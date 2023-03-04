# pnpm-turborepo-vite-azure-static-web-apps

A GitHub template to quickly get started with Azure Static Web Apps, Turborepo, React (Vite) and pnpm.

## Deployment

When you use the Azure portal to create a new Static Web Application, select custom. After the .yaml file was added to your repository, add the following changes:

```yaml
    # set working directory
    defaults:
      run:
        working-directory: "frontend"
    strategy:
      matrix:
        node-version: [16.x]



      # add build steps
      - name: Check out code
        uses: actions/checkout@v3
        with:
          fetch-depth: 10

      - name: Setup pnpm
        uses: pnpm/action-setup@v2
        with:
          version: 7

      - name: Setup node with cache
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
          working-directory: frontend
          cache: pnpm
          cache-dependency-path: "**/pnpm-lock.yaml"

      - name: Install Dependencies
        run: pnpm install --frozen-lockfile

      - name: Build
        run: pnpm build


          # custom build configuration
          app_location: "frontend/apps/app/dist"
          api_location: ""
          output_location: ""
          skip_app_build: true
```
