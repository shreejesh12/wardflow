# WardFlow - Isolation Ward Manager (prototype)

Live demo: https://wardflow-phi.vercel.app

A functional prototype for managing a 74-bed quarantine & treatment facility.
Built as a zero-dependency single-page app (`index.html` - vanilla HTML/CSS/JS,
no build step). All data is synthetic and generated locally in the browser
(localStorage); there is no backend and no real patient data.

## Roles & workflows

- **Nurse**: daily board (temps recorded vs due), records temperatures with
  range validation (34-43C). A second recording the same day is saved as a
  correction - the earlier reading stays in history, marked superseded.
- **Doctor**: review queue sorted so patients with a fresh reading come first;
  logs visits with treatment + notes; a visit before any reading is flagged;
  can recommend discharge only when the patient has 3 full consecutive
  fever-free days on record (a fever recorded today resets eligibility);
  can mark a patient deceased.
- **Admin**: discharge queue re-validates the 3-day criterion before every
  discharge (a broken streak blocks discharge and returns the patient to the
  doctor); admits new patients into freed beds (blocked at full capacity);
  quality tab tracks mortality against the 15% benchmark with an escalation
  warning when exceeded.

## Demo shortcuts

Deep links sign in directly: `#nurse`, `#doctor`, `#admin`
(optionally with a tab, e.g. `#doctor/review`, `#admin/quality`).

Every visitor gets a freshly seeded ward (74 patients, temperature histories,
56 historical outcomes), so the full daily workflow is demonstrable end to end.

## Deploy

Static hosting: `npx vercel deploy --prod` (or drag `index.html` onto any
static host).
