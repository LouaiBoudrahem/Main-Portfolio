LOUAI BOUDRAHEM - 3D GAME DEV PORTFOLIO
=======================================

  index.html          the whole site (three.js r128 is bundled inside it)
  assets/             screenshots, tech icons, favicon, sound icons
  assets/majula.mp3   the background track
  start-portfolio.bat double-click this to run it locally
  serve.ps1           the no-install fallback server it uses
  models/castle.glb  Castel del Monte, the world that rotates
  models/dragon.glb  the dragon: mesh + Idle/Fly animations, merged
  models/sky.glb     the backdrop sphere


RUN IT LOCALLY
--------------
Browsers refuse to load .glb over file://, so double-clicking index.html
will show the low-poly stand-ins instead. It has to be served.

Easiest: double-click  start-portfolio.bat

It looks for Python, then Node, and if neither is installed it falls back to
serve.ps1 - a small static server written in PowerShell, which ships with
Windows. Nothing to install either way. A "Portfolio server" window opens and
your browser goes to http://localhost:8000/ ; close that window to stop.

If you'd rather type it yourself and you do have Python:

    py -m http.server 8000

or, with no Python at all:

    powershell -ExecutionPolicy Bypass -File serve.ps1


PUT IT ONLINE
-------------
Any static host works: GitHub Pages, Netlify, Cloudflare Pages, itch.io.
For itch.io: zip the CONTENTS of this folder (index.html at the top level,
not inside a subfolder) and tick "This file will be played in the browser".


MUSIC
-----
The speaker button sits in the lower left corner. The track plays on load,
looping, fading in over 1.5 seconds. Clicking the button fades out and
pauses; clicking again resumes.

Filenames are case sensitive once the site is on a real host, even though
Windows does not care locally. The file is assets/majula.mp3 in lowercase
and CONFIG.audio.src matches it exactly, so keep them in step if you rename.

The soundon / soundoff icons were recoloured from their original purple to
the site green, keeping the white glyph and its anti-aliasing.


THEME
-----
The palette lives in the :root block at the top of index.html - three
variables drive nearly everything:

  --leaf   #86c96e   primary, new growth
  --amber  #e2a33c   secondary, low sun
  --moss   #4f8f5c   tertiary, canopy

Section accents (CONFIG.checkpoints[].accent) and project colours
(CONFIG.projects[].theme) are per-item hex values. CONFIG.fit.skyTint
grades the backdrop - 0xffffff gives raw daylight, lower/greyer values
push it hazier.


EDIT IT
-------
Everything you'll want to change is in the CONFIG block at the very top of
index.html, so there's no need to scroll past it.

  CONFIG.profile      your name, role, email, header links
  CONFIG.audio        the background music. `src` is the file path, `volume`
                      is 0 to 1, `autoplay` can be set to false to make the
                      visitor press play. Browsers refuse to start audio
                      before the visitor interacts with the page, so when
                      autoplay is refused the track starts on the first
                      click, tap or key press instead. If the file is
                      missing the toggle greys out and nothing breaks.
  CONFIG.experiences  the Experience timeline - title / company_name / icon /
                      iconBg / date / points, same field names as your React
                      constants array. Cards slide in alternately from left
                      and right as they scroll into the panel; the animation
                      replays each time the section is opened. `points` is an
                      array, so a role can list several bullets.
  CONFIG.skills       the Skills list - imageUrl / name / type, same field
                      names as your React constants array. Icons live in
                      assets/; a few upstream logos are solid black, so
                      white variants are used (unity-white.png,
                      express-white.svg, social-github.svg). blender.png was
                      keyed off a baked-in transparency checkerboard and
                      cropped square; claude.png was cropped and squared.
  CONFIG.socials      the cards in the Socials section - label, handle,
                      icon, url, accent. Icons live in assets/ as white SVGs
                      so they read on the dark panel.
  CONFIG.checkpoints  the six sections. Add or remove entries and the
                      beacon ring re-spaces itself automatically.
  CONFIG.projects     the cards shown in the Projects panel. Same field
                      names as your React constants array - iconUrl / theme /
                      name / description / link - except `theme` is a hex
                      colour instead of a CSS class, and `imageUrl` is
                      optional (cards without one just show no screenshot).
                      Add a project by appending to the array; drop its
                      screenshot in assets/ and point imageUrl at it.
  CONFIG.projectsIntro  the paragraph above the cards. It's clamped to three
                      lines with a "Read more" toggle so the projects stay
                      near the top of the panel.
  CONFIG.fit          scale and placement of castle / dragon / sky, plus
                      skyTint. Set it to 0xffffff for the original
                      daylight sky instead of the graded dusk.
  CONFIG.clips        both dragon states run the SAME Fly cycle: idleSpeed
                      (0.45) is a slow hover, flySpeed (1.45) is turbulent
                      flight while you turn the castle. `turbulence` adds
                      procedural roll/pitch/buffet on top - set it to 0 for
                      steady flight. The separate Idle clip is still inside
                      dragon.glb: point CONFIG.clips.idle at ["idle"] and the
                      code detects two clips and crossfades instead.


HOW THE ASSETS WERE PREPARED
----------------------------
  castle   58.0 MB -> 7.4 MB   16384px texture downsampled to 4096,
                               geometry simplified to 30% (500k -> 150k tris)
  dragon   13.9 MB -> 4.1 MB   Dragon.fbx + Dragon@Idle.fbx + Dragon@Fly.fbx
                               converted to one glTF (Dragon.fbx holds no
                               animation of its own - both clips were grafted
                               onto its skeleton by bone name, 876 channels
                               each, none dropped); DDS textures re-encoded to
                               JPEG @1024; animations resampled
  sky      11.8 MB -> 2.2 MB   4096x2048 PNG re-encoded as JPEG

The originals are untouched in your Portfolio folder.
