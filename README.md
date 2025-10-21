# Astro Bug Minimal Reproduction

In the latest versions of Astro at the time of writing (5.14.x), images that are imported in Astro components and rendered via the `<Image>` component will fail to load **if** the folder that Astro site
was built to is moved to a new location before being run. This is a common use case for developers, including my usecase of self-hosting on a VPS using Dokku.

### Steps to Reproduce

1. Install dependencies `pnpm install`

2. Build site `pnpm build`

3. Run site as docs say for production `node ./dist/server/entry.mjs`
    - At this point you should see the 1 page with the "Hello World" image properly rendered at http://localhost:4321/

3. Kill server and move the created `dist/` folder somewhere else `mkdir deployment && mv dist deployment`

4. Run site again ``node ./deployment/dist/server/entry.mjs`
    - **Clear your browser cache so the image is not stored still**
    - The image will fail to render, and opening the path to it in a new tab will show `Internal Server Error`