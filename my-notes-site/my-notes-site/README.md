# My Notes

A simple website for keeping course notes, organized by subject.

## Structure

```
my-notes-site/
  index.html            <- homepage, lists all subjects
  style.css              <- all styling, one file
  subjects/
    imc.html
    entrepreneurship.html
    organisational-behaviour.html
    business-law.html
    financial-management.html
    business-finance-2.html
```

Each subject page holds all of that subject's chapters, newest at the top.

## Adding a new chapter each week

Chapters don't hold the actual notes — each one is just a title, a date, and
a link out to the real document (a Google Doc or a Word file). That way your
notes stay editable in whatever app you already write them in.

1. Open the subject's HTML file in `subjects/`.
2. Copy one `<section class="chapter">...</section>` block.
3. Paste it at the **top** of `<main class="chapters">`, give it a new `id`
   (e.g. `ch2`), bump the chapter number, update the title and date.
4. Update the `href` on the `.chapter-link` to point at that week's document
   — see the two options below.
5. Add a matching link at the top of the `<nav class="chapter-nav">` list.
6. Save, refresh the page in your browser to check it looks right.

### Option A — link to a Google Doc (easiest)

1. Write your notes in Google Docs as usual.
2. Click **Share > General access**, set it to "Anyone with the link", and
   make sure the role is "Viewer" (or "Commenter" if you want friends to
   comment).
3. Copy the link and paste it into the `href`:
   ```html
   <a
     class="chapter-link"
     href="https://docs.google.com/document/d/XXXXXXXX/edit"
     target="_blank"
     rel="noopener"
   >
     Open full notes &middot; Google Doc
   </a>
   ```

### Option B — link to a Word file that lives in the project

1. Create a `notes/` folder next to `index.html`, and inside it a folder per
   subject, e.g. `notes/imc/chapter-1.docx`.
2. Drop your `.docx` file there.
3. Point the link at it with a relative path, and add `download` so it
   downloads instead of trying (and failing) to open in the browser:
   ```html
   <a class="chapter-link" href="../notes/imc/chapter-1.docx" download>
     Download notes &middot; Word file
   </a>
   ```
4. Because this file gets pushed to GitHub along with everything else, it
   works the same way once the site is live online.

Google Docs are simpler to keep updated (edit in place, link never changes).
Word files are better if you want the notes to work fully offline.

## Adding a brand-new subject

1. Copy any file in `subjects/` and rename it, e.g. `subjects/statistics.html`.
2. Delete the extra chapter sections, keep one, and edit it.
3. Pick a color for `style="--spine: #______"` in the `<body>` tag — this is
   the subject's accent color throughout that page.
4. Go to `index.html`, copy one `.subject-row` block, point its `href` at
   your new file, and give it the same spine color.

## Viewing it locally

Just open `index.html` in your browser — no server needed for this simple
setup. In VS Code, the "Live Server" extension is a nice add-on: it
auto-refreshes the page whenever you save a file.

## Putting it online so friends can see it (GitHub Pages, free)

1. Create a GitHub account if you don't have one, and create a new repository
   (e.g. `my-notes`).
2. In VS Code's terminal, from inside this folder:
   ```
   git init
   git add .
   git commit -m "first version of notes site"
   git branch -M main
   git remote add origin https://github.com/swano4519-code/NoteForKeeping.git
   git push -u origin main
   ```
3. On GitHub, go to the repo's **Settings > Pages**, set the source to the
   `main` branch, and save.
4. After a minute, your site is live at
   `https://YOUR-USERNAME.github.io/my-notes/`. Share that link with friends.
5. Every week: edit your HTML files, then run
   ```
   git add .
   git commit -m "add chapter 4 notes"
   git push
   ```
   and the live site updates automatically within a minute or two.
