# All Things Leland Events Calendar: Editorial Workflow

## Two lists

- `data/review-queue.json`: proposed events awaiting editorial review. Items here are not approved for publication.
- `data/events.json`: approved events intended for publication on the calendar.

## Required fields for each event

```json
{
  "id": "unique-short-id",
  "title": "Event title",
  "category": "Government Meeting",
  "start": "2026-10-26T18:00:00-04:00",
  "end": null,
  "venue": "Venue name and town",
  "description": "Brief factual description",
  "source_url": "https://official-host.example/event",
  "source_name": "Official event host",
  "status": "pending",
  "checked_at": "2026-10-17",
  "editor_note": "Any ambiguity or details to confirm"
}
```

Use ISO 8601 dates with the local North Carolina offset. Set `end` to null when the end time is not published. Never guess a date, time, address, cost, or registration requirement.

## Daily review process

1. Research official Town of Leland, Brunswick County, school, library, and event-host calendars first.
2. Add newly found items to `data/review-queue.json`, including the official source URL and the date checked.
3. Review the event details and open the source link. Confirm date, time, venue, public access, and registration requirements.
4. For approved events, move the item to `data/events.json`, set `status` to `published`, and remove any unresolved editor note.
5. Remove expired events from `data/events.json`. Keep uncertain, changed, or cancelled items in the review queue until resolved.
6. Commit the update to the `main` branch. GitHub Pages will deploy when the repository's Pages workflow runs.

## Approval policy

The current workflow is **editor-approved publishing**. A scheduled research task can prepare suggestions, but it is not yet connected to commit files to this repository. Do not describe daily publication as automatic until that connection is implemented and tested.

## Important implementation note

The two JSON files establish the data and review structure. The current website still contains its existing HTML event cards; the next implementation step is to make the page render approved entries from `data/events.json` and keep review-queue items off the public calendar.
