# How to update the site

Everything is edited directly on github.com in a web browser. Each saved
change ("commit") rebuilds the site automatically; the live page updates
in about a minute. No software is required on your computer.

## Add a talk

1. Open the `_talks` folder in this repository on github.com.
2. Open `TEMPLATE.md` and copy its contents.
3. Go back to `_talks`, choose **Add file → Create new file**.
4. Name the file `YYYY-MM-DD-lastname.md`, using the talk date,
   for example `2026-10-12-rivera.md`.
5. Paste the template, fill in the fields between the two `---` lines,
   and **delete the `template: true` line**.
6. Press **Commit changes**.

Rules that keep the build happy:

- `date:` must be written `YYYY-MM-DD`.
- Keep the quotes around `title:` — a title containing a colon breaks
  the page without them.
- `semester:` must match the other entries for that semester exactly
  (for example `Fall 2026`), because it is what groups the schedule.
- Leave `room: ""` to show the default venue; type a room to override it.
- If a field does not apply (no host yet), delete the whole line.

## Slides and recordings

After a talk, open its file in `_talks`, press the pencil icon, and add
either or both lines between the two `---` lines:

```
slides: https://example.edu/slides.pdf
recording: https://example.edu/recording
```

The schedule then shows **Slides** and **Recording** links in that
talk's row. A slides file can also be uploaded to the repository (for
example to a `slides` folder) and given as `slides: slides/rivera.pdf`.
Leave a field empty, or leave the line out, and no link is shown.

## Hide a talk

To keep a talk off the website and out of the calendar feed — for
example while it is not yet confirmed — add this line to its file:

```
hidden: true
```

The talk disappears from the schedule, the "Next up" card and the
calendar feed. Its flyer address still exists but only says "This talk
is not available", and its PDF is removed. Delete the line, or set
`hidden: false`, to show it again. Note that the file itself is still
visible to anyone who looks at this repository on GitHub.

## Cancel a talk

Open the talk's file in `_talks`, press the pencil icon, and add the line

```
cancelled: true
```

between the two `---` lines, then commit. Keep the file — do not delete
it. The schedule then shows the talk with a red **Cancelled** tag (the
"Next up" highlight and home-page flyer move on to the following talk),
the flyer and its PDF get a large diagonal **CANCELLED**, and the talk is
removed from the calendar feed. To undo, delete the line or set
`cancelled: false`.

## The calendar feed

The site publishes every talk as a calendar people can subscribe to, at
`https://fiu-bio-seminar.github.io/calendar.ics` (linked from the home
page as "Subscribe to the calendar"). It updates by itself whenever a
talk is added, edited, or cancelled. Subscribers' calendar apps check
for changes on their own schedule — Google Calendar can take up to a
day — so a late change may not reach everyone immediately.

## A week with no seminar

Create the file with only three fields:

```
---
semester: Fall 2026
date: 2026-11-23
note: "No seminar (Thanksgiving break)"
---
```

## The flyer

The flyer on the home page is generated automatically from the next
upcoming talk's entry: it shows the site banner, the speaker's photo,
name, affiliation, the talk title, and the date and room. Nothing
needs to be designed or uploaded week to week — the flyer rotates on
its own as each talk date passes.

To add the speaker's photo:

1. Open the `images` folder, choose **Add file → Upload files**, and
   upload the photo (square photos work best; name it after the
   speaker, for example `rivera.jpg`).
2. Open that talk's file in `_talks`, press the pencil icon, and set
   `photo: images/rivera.jpg`.
3. Commit.

Instead of uploading, `photo:` can also be a full link to an image on
another site, for example
`photo: https://example.edu/people/rivera.jpg` (use the address of the
image itself, ending in `.jpg`, `.png`, etc., not of a web page). The
same works for team photos in `_data/team.yml` and the flyer logo in
`_data/site.yml`. A copy in `images/` is more reliable: a linked image
disappears if the other site moves it, and some sites block their
images from being shown elsewhere.

If a talk has no `photo:` line, or its image cannot be loaded, the
flyer shows the speaker's initials instead.

## The printable flyer

Every talk also gets a letter-size flyer page, built automatically
the moment the talk's file is committed. It is linked from the talk's
row on the schedule ("Flyer") and from the home-page card ("Printable
flyer"), and lives at `flyers/YYYY-MM-DD-lastname.html`.

A PDF of each flyer is also made automatically: a few minutes after a
talk is added or edited, a robot commit ("Update flyer PDFs") saves
`flyers/YYYY-MM-DD-lastname.pdf`, and the flyer page gains a
**Download PDF** link. Progress shows on the repository's **Actions**
tab, under "Flyer PDFs". The **Print / Save as PDF** button on the
flyer page works any time, too.

The flyer uses these fields from the talk's file:

- `title:` and the optional `subtitle:` (printed as a second line)
- `date:`, plus `start:` and `end:` — 24-hour times in quotes, such as
  `start: "12:00"` and `end: "13:30"`; leave them out to use the usual
  seminar times from `_data/site.yml`
- `zoom:` (optional) — the talk's Zoom link; leave it out to use the
  default `zoom:` from `_data/site.yml`, or write `zoom: false` for none
- `speaker:`, `affiliation:`, `photo:`
- the abstract, written below the second `---`
- `link:` (optional, e.g. the speaker's web page) — printed in the footer
- `host:` (optional) — printed in the footer

The banner text and logo are set once in `_data/site.yml`
(`flyer_series:` and `flyer_logo:`). Long titles and abstracts are
shrunk automatically to keep the flyer on one page.

## Edit the team or the links

- Team page: edit `_data/team.yml`. Photos go in `images/`.
- Links page: edit `_data/links.yml`.
- Site name, year, venue, default start/end time, default Zoom link,
  contact address: edit `_data/site.yml`.
- Which semesters the home page shows: edit `semesters:` in
  `_data/site.yml` (for example to hide past semesters). An empty list,
  `semesters: []`, shows all of them. Hidden talks keep their flyers and
  stay in the calendar feed.

In these files, keep the indentation and the quotes exactly as they
are and change only the text between the quotes.

## If the site did not update

A broken build sends an email to whoever made the last commit. The
usual causes are a missing quote, a date not written `YYYY-MM-DD`, or
changed indentation in a `_data` file. Open your last edit, compare it
against `TEMPLATE.md` or the neighboring entries, and commit a fix.
