# Import map issue with Deno VSCode extension

This repo is a minimal repro for a Deno VSCode extension issue with import maps.  
(last checked with VSCode v1.53.2, Deno extension v3.1.0, and Deno v1.8.0 on Windows 10)

I'm using an import map to remap `.js` imports to `.ts` in code I share between the browser and Deno.
(This itself is not a great solution but it's the only one I've found)

The code is working in Deno and the import map is doing its job, since this works without error:

    deno run --import-map=importMap.json server/mod.ts

But if you open the repo folder in VSCode and open `browser/shared.ts`, the Deno extension complains with:

    Unable to load a local module: "file:///c%3A/Users/elisee/Desktop/vscode-deno-import-map/browser/secondary.js".
    Please check the file path.

As a consequence, you'll also get the following error in `server/mod.ts`:

    Property 'value' does not exist on type 'typeof import("file:///c%3A/Users/elisee/Desktop/vscode-deno-import-map/browser/shared")'.

So somehow **the import map is not being applied properly by the Deno VSCode extension**.

Any help in getting this to work would be greatly appreciated!
