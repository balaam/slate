## Dinodeck Docs

The files to edit are ./index.html.md and all the files in the `include` directory.

### Tool

The documentation is built using [Slate](https://github.com/lord/slate).

### Build

To build run this command

    bundle exec middleman build --clean

That will put all the static files into the `build` folder.

### Test Build

You can open ./build/index.html to test it out.

### Deploy

We're deloying to `dinodeck.com/docs` and this is available in `../dinodeck.com`.

There's a handy rake command to update it.

    rake update_docs