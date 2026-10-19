# All Things Leland Events Calendar: Editorial Workflow

## Two lists

- `data/review-queue.json`: proposed events awaiting editorial review. Items here are not approved for publication. This is the canonical review queue.
- `data/events.json`: approved events intended for publication on the calendar.

## Daily review and approval

1. Research official Town of Leland, Brunswick County, school, library, and event-host calendars first.
2. Add newly discovered listings and proposed corrections to `data/review-queue.json`, including an official source URL and the date checked. Do not duplicate events already in either file.
3. Present the review package to the editor with clear proposed additions, corrections, and any details that need checking.
4. The editor responds **Approve** or **Disapprove** for each proposal (or says **OK** to approve the clearly identified batch).
5. For approved additions, move the item into `data/events.json` and set `status` to `published`. For disapproved items, do not publish them; remove them from the pending queue or mark them disapproved in the review record. Keep unresolved listings pending.
6. Commit approved changes to the `main` branch. GitHub Pages deploys when repository changes are pushed. Never treat a review response as published until the GitHub change and deployment have actually occurred.

## Required fields for each event

```json
{
  "id": "unique-short-id",
  "title": "Event title",
  "category": "Community event",
  "start": "2026-10-26T18:00:00-04:00",
  "end": null,
  "venue": "Venue name and town",
  "description": "Brief factual description",
  "source_url": "https://official-host.example/event",
  "source_name": "Official event host",
  "status": "pending",
  "checked_at": "2026-10-19",
  "editor_note": "Any ambiguity or details to confirm"
}
```

Use ISO 8601 dates with the local North Carolina offset. Set `end` to null when the end time is not published. Never guess a date, time, address, cost, or registration requirement.

## Automatic removal of past events

- A scheduled GitHub Actions workflow runs daily and removes expired entries from `data/events.json`. It uses the event end time when available, otherwise the start time.
- The public page also hides expired events immediately, so an old listing will not remain visible while the cleanup workflow is waiting to run.
- The cleanup workflow commits changes only when it finds expired events. That commit triggers the regular GitHub Pages deployment.
- Malformed dates are retained rather than silently deleted, so they can be corrected by an editor.

## Publishing and safeguards

Publishing remains editor-approved: newly discovered events must stay in the review queue until the editor approves them. Expired-event removal is automatic. The scheduled research task prepares the review package; it is not itself a confirmed direct GitHub writer, so an assistant with authorized GitHub access must apply approved additions and corrections.

The public page reads approved entries from `data/events.json` and does not display pending review-queue items. Preserve the existing banner, introduction, official-calendar links, verification note, category ordering (Community Events first), and footer.
