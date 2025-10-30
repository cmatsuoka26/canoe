# Canoe Planter — README

Short static site about traditional canoe plants and the Punahou capstone project.

## Quick start

- Open the site in a browser (some features require HTTP):
  - Using Python (macOS):
    - cd to the project root:
      ```bash
      cd /FileLocation/
      python3 -m http.server 8000
      ```
    - Open http://localhost:8000
  - Or use VS Code Live Server.

## Project overview

- Static HTML/CSS with a small client-side JS embedded in pages.
- Data source: [plants.json](commonAssets/plants.json) — used by the search and plants dropdown.
- Navigation:
  - Each page has an off-screen hamburger menu (`.off-screen-menu`) and search overlay (`.off-screen-search`).
  - The "Explore" item in those menus should point to the plants grid page: [index.html](plants/index.html).
  - The center/home logo (nav-logo) on plant pages should link back to the site root home: [index.html](index.html) (use `href="../index.html"` from plant subfolders).

## File / Folder map (important files)

- Root
  - [index.html](index.html)
  - [style.css](style.css)
  - [plants.json](commonAssets/plants.json)
- Plants section
  - [index.html](http://_vscodecontentref_/6)
  - [style.css](http://_vscodecontentref_/7)
- Plant pages
  - Kalo: [index.html](kalo/index.html) + [style.css](kalo/style.css)
  - Ko: [index.html](ko/index.html) + [style.css](ko/style.css)
  - Niu: [index.html](niu/index.html) + [style.css](niu/style.css)
  - Noni: [index.html](noni/index.html) + [style.css](noni/style.css)
  - Ulu: [index.html](ulu/index.html) + [style.css](ulu/style.css)
- About
  - Our Mission: [index.html](ourMission/index.html) + [style.css](ourMission/style.css)
  - Team Members: [index.html](teamMembers/index.html) + [style.css](teamMembers/style.css) + email list [s.html](teamMembers/s.html)

## How navigation works / troubleshooting

1. Off-screen menu and search rely on elements existing in the DOM:
   - script queries used across pages: `.ham-menu`, `.off-screen-menu`, `.search-icon`, `.off-screen-search`
   - If clicking hamburger/search does nothing:
     - Open the browser console and check for errors (e.g., `searchIcon is null`).
     - Ensure the HTML contains elements with those classes/IDs and that the embedded script runs after those elements (scripts are included at bottom of pages).
2. Home logo behavior:
   - On plant subpages the logo should use a relative path back to home:
     - Example in kalo [index.html](kalo/index.html):
       ```html
       <a href="../index.html" class="nav-logo no-select"><img src="../commonAssets/punLogo.svg" alt="Punahou Logo"></a>
       ```
   - If logo does not navigate, check that `href` is correct for that page depth and that there are no JavaScript handlers calling `preventDefault()` on the logo link.
3. "Explore" menu item:
   - Ensure every off-screen menu dropdown has:
     ```html
     <li><a href="../plants/index.html">Explore</a></li>
     ```
     from subfolders, or [index.html](index.html) from root pages.

## Adding a plant

1. Add entry to [plants.json](commonAssets/plants.json):
   - Example:
     ```json
     {
       "name": "newplant",
       "other_names": ["alias"],
       "howto": "Usage notes",
       "url": "/canoe/newplant/index.html"
     }
     ```
2. Create [index.html]() and [style.css]().
3. Add a `.box` link in [index.html]() to the new page.

## Common fixes

- Search results empty / fetch errors:
  - Serve via HTTP (file:// fetch may be blocked). Use `python3 -m http.server` or Live Server.
  - Verify `fetch('../commonAssets/plants.json')` path is correct relative to the page.
- Duplicate navbars / mismatched behavior:
  - Remove duplicate nav markup — ensure only one `<nav>` per page.
  - Ensure CSS selectors for `.nav-left`, `.nav-right`, `.nav-logo` are consistent across pages.
- Missing assets (icons, images):
  - Confirm relative paths like `../commonAssets/punLogo.svg` or `./menuIcon.svg` are correct from the page location.

## Contributing

- Keep per-page CSS in each folder.
- Keep shared data in [commonAssets](/commonAssets/).
- When changing nav markup, update all pages to keep behavior consistent.

