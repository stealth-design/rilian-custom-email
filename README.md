# Rilian VIP Invite — HTML email

Event invitation for **For Those Shaping the Future of OT and Critical Infrastructure Security**
Rove Hotel, Expo Dubai South · Wednesday 16 September 2026, 16:00–18:00

## Files

| File | Purpose |
|---|---|
| `invite.html` | The email. Table-based, inline styles, ready to send. |
| `preview.html` | Local preview with a one-click "Copy for Gmail / Outlook" button. |
| `images/` | Source copies of the four hosted assets. |

## Sending

Open `preview.html` on a local server (the Clipboard API needs a secure context, so
`127.0.0.1` works but `file://` does not), click **Copy for Gmail / Outlook**, and paste
into a compose window.

For an ESP, paste the whole of `invite.html` into a "code your own" campaign — that keeps
the `<style>` block, which Gmail's compose sanitiser strips.

Set a subject line. The email has no `<title>` on purpose: Gmail discards `<head>` but
renders text found inside it, which leaked the title into the body.

## How it is built

The invite artwork is one design sliced into three, so a live RSVP button can sit in the
empty band at the centre of the card:

- `card-top` → headline and above
- `card-band` → used as the *background* of the button row, so the pattern runs unbroken
- `card-bottom` → venue, date, RSVP line

Both card halves and the button link to `mailto:events@rilian.com` with the subject
pre-filled. Assets are hosted on Cloudinary; the URLs are versioned, so re-uploading
revised artwork produces new URLs rather than updating these in place.

## Client notes

- **Outlook** — the band background and the button both fall back to VML, so they render
  even with images blocked.
- **Dark mode** — `prefers-color-scheme` plus `[data-ogsc]` locks hold the palette in Apple
  Mail and Outlook. The Gmail app ignores both and force-recolours CSS; the button survives
  there only because it is an image, and forced dark mode never recolours images.
- **Images blocked** — the alt text on each slice carries the full date, time and venue.
