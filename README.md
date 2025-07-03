# esbuild-glob-symlinks
## Bug repro for esbuild

### Bug description

When using a `/**/` [glob pattern for entry
points](https://esbuild.github.io/api/#glob-style-entry-points), symlinked
directories seem to be completely ignored. This is true with or without
`--preserve-symlinks`. The included example uses `--preserve-symlinks` because
it seems more correct: my understanding is it means "treat symlinks as if they
were files or directories in the location of the symlink". Instead, esbuild
seems to act as if the symlink is not there.

### To reproduce

Check out this repo, then
```
npm install
npm run build
```
This will create a new directory called `dist/`.

### Expected behavior

I expected the `dist/` directory to have this structure:

* dist/
  * index.js
  * nested/
    * nested.js
  * linked/
    * linked.js

### Actual behavior

Directory `dist/linked/` is not created, so the entire directory is:

* dist/
  * index.js
  * nested/
    * nested.js
