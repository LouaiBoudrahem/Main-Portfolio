# Louai Boudrahem | 3D Game Developer Portfolio

An interactive portfolio built with three.js. A castle rotates at the centre of a
mountain scene while a dragon flies above it. Each beacon on the ring opens a
section: projects, experience, skills, about and socials.

**Live:** https://louaios.github.io/portfolio/

## Built with

- three.js r128 (bundled inline, no build step and no dependencies)
- glTF models exported from Blender, optimised for the web
- Plain HTML, CSS and JavaScript in a single file

## Running it locally

Browsers block `.glb` loading over `file://`, so the folder has to be served:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000/

## Structure

```
index.html      the whole site, including the bundled three.js
models/         castle, dragon and sky, all glTF binary
assets/         screenshots, tech icons, favicon, music
```

Everything editable lives in the `CONFIG` object at the top of `index.html`:
profile, projects, experiences, skills, socials, model placement and theme.

## Credits

- Castle model: Castel del Monte, from Sketchfab (add the author and licence here)
- Dragon model and animations: (add the source here)
- Skybox: (add the source here)
- Music: Majula, from Dark Souls II by FromSoftware
