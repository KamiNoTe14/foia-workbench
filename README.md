# FOIA Calendar Review

A free, offline tool for school districts (and other public bodies) to review a Google Calendar export for a public-records request, redact exempt information, and produce a clean release copy.

**[Open the tool →](https://kaminote14.github.io/foia-calendar-review-tool/)**

## Why this exists

When a FOIA request asks for someone's calendar, Google Vault can export it as an `.ics` file. Most ICS viewers show only the title, date and time. They drop the guest list and each guest's response, and give you no way to redact anything. This tool reads the full export and lets a FOIA coordinator mark redactions. It then exports a release copy where redacted text is **actually removed**, not just covered with a black box.

## Your data never leaves your computer

This is a single HTML page with no server, no analytics and no outside scripts. When you open the `.ics`, the browser reads it locally and all processing happens in that browser tab. The page works the same whether you open it from this site or download `index.html` and double-click it. You can confirm this by checking the browser's Network tab, which shows no requests after the page loads.

## What it does

- **Reads the full Vault `.ics` export**, including:
  - guests and their responses (Accepted / Declined / Maybe / No response)
  - organizer, location and description
  - repeating events, expanded into the requested date range
  - time-zone and daylight-saving conversion
- **Separates conference boilerplate** (Google Meet, Teams, Zoom join links and dial-in PINs) into its own field so it can be redacted in one click.
- **Suggests redactions without applying them.** The coordinator approves or dismisses each one. Suggestions cover:
  - meeting links, passcodes and PINs
  - personal email addresses (Gmail, Yahoo, etc.)
  - possible student accounts
  - medical appointments
  - staff birthdays and anniversaries
- **Flags items for review:** suspected calendar-phishing invites, and entries that mention personnel or legal matters (FMLA, appeals, attorneys, etc.).
- **Redacts at any level:**
  - a whole field
  - one guest
  - highlighted words
  - an entire entry (withheld in full)
- **Exports:**
  - **Release copy → PDF** (print / Save as PDF) with a request header and a list of the exemptions cited
  - **Review copy for markup → Print**: an internal, unredacted printout for people who review on paper. Planned redactions are highlighted with their exemption code, suggestions and warnings are listed under each entry, and it's stamped *Not for release*.
  - **Print one calendar entry per page**: a checkbox in the Export menu that works with both print options. In the review copy, each page also gets a notes box with release / redact / withhold checkboxes and initials.
  - Printed pages leave out the browser's URL and date header. If they still appear, uncheck *Headers and footers* under *More settings* in the print dialog.
  - **Release copy → CSV** for Excel
  - **Exemption summary**, a paragraph to adapt for the written response
  - **Internal redaction log (CSV)**, which includes the original text and is for the coordinator's file only
- **Save / open project:** one `.json` file holds the calendar plus every redaction, so several people can hand the review back and forth.

## How to use it

1. In Google Vault, export the person's calendar for the date range and download the `.ics`. The PST export holds the same events; use the `.ics`.
2. Open the tool and drop in the `.ics`.
3. Set **From** and **To** to match the request.
4. Pick an exemption in **Redact as**, then redact using the ⊘ buttons, **Redact selection**, or **Withhold entry**. Review the suggestions and apply or dismiss each one.
5. Click **Save project** often. The `.json` file contains the unredacted calendar, so store it like the original export.
6. Use **Release preview** to check the result, then **Export → Release copy → Print / Save as PDF**.

## Exemptions and other states

The built-in exemption list is the **Michigan FOIA, MCL 15.243(1)**: (a), (d), (g), (l), (m), (u), (y), (z). In other states, use **Redact as → + Add another exemption** and enter your statute's full citation and a general description. Custom exemptions are saved in the project file. The exemption summary and PDF header mention Michigan statutes; adjust that wording for your state before sending.

> **Not legal advice.** The suggestions are pattern matches, not legal determinations. Whether an exemption applies is up to your FOIA coordinator or counsel.

## A note on "attendance"

Calendar data records each guest's *reply to the invitation*. It does not show who actually attended. The release copy says so in its header.

## Security tip

If the review turns up phishing invites (fake "document shared with you" or "agreement to review" events from outside senders), that's a separate problem worth fixing. In the Google Workspace admin console, consider limiting which invitations are added to calendars automatically.

## Never commit data to this repo

The included `.gitignore` blocks `.ics`, `.pst`, `.json`, `.csv` and `.pdf` files. Keep it that way: this repo is public, and calendar exports belong on district storage.

## License

MIT. Free to use, modify and share. Pull requests are welcome, especially exemption presets for other states.
