# Golf Achievement — Funnel and Follow-Up Starter

Status: proposed architecture and unsent copy. No platform configured. All workflows OFF.

## Two routes

Content/referral → relevant brand page → Next-Round Scorecard → choose local or online interest.
Local → validated booking destination → booked → attended → suitable coaching offer → active golfer.
Online → confirmed program page → checkout → payment confirmed → member access → first practice task → progress review.
Keep source, route, and offer IDs distinct so the two paths can be measured separately. A discovery call is not required for every self-paced purchase.

## Fields and proposed tags

Fields: lead ID, email, preferred name, origin domain, source, route, goal, stage, consent state/date/source, booked date, assigned owner, next action/date. Avoid collecting unnecessary sensitive data.
Tags: ga:interest:local, ga:interest:online, ga:asset:scorecard, ga:stage:booked, ga:stage:enrolled, ga:suppress:marketing. Stage and consent fields are authoritative; tags mirror them, never override them.

## Trigger map

| Event | Proposed action | Stop/exit condition |
|---|---|---|
| Scorecard requested | Deliver asset; record request | Duplicate submission should not duplicate delivery |
| Separate marketing opt-in | Start education sequence | Unsubscribe, hard bounce, or manual suppression |
| Booking confirmed | Stop booking asks; send correct confirmation | Cancellation replaces old reminders |
| Purchase confirmed | Stop acquisition sequence; issue correct access | Failed payment must not grant paid access |
| No-show | One contextual reschedule message | Rebooked, declined, or suppressed |
| Reply arrives | Assign human follow-up | Pause scheduled sales asks until handled |

Transactional confirmations and marketing messages need separate rules. Respect the user's recorded preference across both domains.

## Four draft emails

**1 — Delivery, immediately after request**
Subject: Your Next-Round Scorecard
Here is the scorecard you requested: [validated download link]. After your next round, choose one pattern you would like to change. Keep the notes for your next practice session. — Brad

**2 — Education, proposed two days later; marketing opt-in only**
Subject: Choose one practice priority
Look at your scorecard. Which pattern repeated most often? Choose one priority and decide how you will observe progress. Keep the task small enough to repeat. If you want help choosing, reply with your golf goal. — Brad

**3 — Route choice, proposed five days later; marketing opt-in only**
Subject: How would you like support?
Some golfers want coaching in person; others prefer to learn online. Explore the confirmed options at [local coaching link] or [online program link]. Choose the format that fits the way you practice. — Brad

**4 — Follow-through, proposed nine days later; marketing opt-in only**
Subject: What changed on your next round?
Compare your notes. What improved, what repeated, and what is your next priority? Progress becomes easier to see when you keep a simple record. If you would like help building your plan, reply and tell me where you want to start. — Brad

Links must be validated and placeholders replaced before use. Add a working unsubscribe mechanism to marketing messages. A direct reply is handled by Brad or an assigned person; no autoresponder is assumed.

## Acceptance checks before activation

Use test identities to verify each consent state, both routes, duplicate submissions, bookings/cancellations, failed/successful payments, replies, suppression, access delivery, and missing required fields. Record results. Confirm sender authentication and send a small controlled test before turning on a live sequence. Do not infer that any of these checks have passed.
