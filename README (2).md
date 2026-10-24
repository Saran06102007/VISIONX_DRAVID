# WorkLink (Web)

**Hyperlocal on-demand blue-collar services marketplace**, built for the Vecnaverse National Level Hackathon (Social Impact domain). This is the plain **HTML / CSS / JavaScript** version of the WorkLink prototype: no build step, no dependencies, no backend.

> Prototype note: all people, prices, ratings, payments and KYC verification are simulated and live in memory. Refreshing the page resets the data.

## Run it

Open `index.html` in any modern browser. That's it.

Or serve it locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

### Deploy on GitHub Pages

1. Push these files to your repo (keep `index.html` at the repo root, with the `css/` and `js/` folders beside it).
2. In the repo go to **Settings -> Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select your branch and `/ (root)`, then **Save**.
4. Your app will be live at `https://<your-username>.github.io/<repo-name>/`.

## Demo logins

Tap **Demo** on the first screen, or use **Sign in**:

| Role | Login | Password |
|------|-------|----------|
| Customer | `aarav@demo.worklink` or `9000000001` | `demo123` |
| Worker | `arjun@demo.worklink` or `9000000002` | `demo123` |
| Student | `nisha@demo.worklink` or `9000000003` | `demo123` |

## Features

| Role | What you can do |
|------|-----------------|
| **Customer** | Browse 9 service categories, discover workers ranked by distance with ETA, filter by availability and verification, change area, request a booking, negotiate price (offer / counter-offer / accept), track live status, chat, pay and review |
| **Worker** | Go online/offline (needs verification), receive requests, accept / counter / decline, advance a job (start travel, start work, complete), view an earnings chart |
| **Student** | Browse and search gigs, apply, get shortlisted then hired (simulated), complete shifts for earnings, set weekly availability slots |
| **Shared** | Dark / light / system theme, notifications, simulated KYC verification with admin override, demo controls |

### What makes it different

- **Two-way pricing:** workers set a rate and customers can counter-offer.
- **Trust first:** "Request nearest" only targets verified, available workers, and declined requests can roll to the next nearest candidate.
- **Distance-ranked with ETA:** workers are sorted by distance (Haversine), ETA is estimated from distance.
- **Student gig mode:** a separate flow for short campus-style jobs.

## Demo controls

Open from the first screen or **Profile -> Demo controls**:

- Auto-respond on / off
- Fast timing (x3)
- Worker reply mode: mixed / always accept / always counter / always decline / no response
- Forced verification outcome
- Theme: dark / light / system

## Suggested 2-minute demo path

1. **Demo controls**: turn on Fast timing and set the worker to *Always counter*. Go back and tap **Demo** under Customer.
2. Tap **Electrician**, open a worker, **Request booking** with a lower offer.
3. A **counter-offer** arrives. Accept it, then watch the status move confirmed -> on the way -> work started -> completed.
4. **Pay**, leave a review, open **Chat** and ask "what is the ETA?".
5. Sign out, tap **Demo** under Worker, go online, tap **Simulate request**, accept it and advance the job, then open **Earnings**.
6. Sign out, tap **Demo** under Student, apply to a gig and watch it become shortlisted then hired.

## Project structure

```
index.html        app shell
css/styles.css    theme (dark/light), layout, components
js/data.js        mock categories, workers (Chennai areas), student gigs, demo accounts
js/logic.js       state + engine: ranking, negotiation, booking state machine, verification, students
js/ui.js          screens, navigation, event handling
```

**Booking lifecycle:** `awaitingWorker` -> `counterReceived` (repeats) -> `confirmed` -> `onTheWay` -> `workStarted` -> `completed` (or `cancelled` / `rejected`).

## Limitations

Hackathon prototype: no real payments, documents, GPS or accounts. Sign-up forms are not included in this web version, so use the demo accounts. A Flutter version of the same prototype also exists.

## Roadmap

Cloud backend and database, live GPS and maps, UPI payments with escrow, e-KYC partner and push notifications, commission-based revenue (proposed).
