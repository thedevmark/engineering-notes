# Building Pathos

Pathos is a job-search system built for the candidate. It brings role discovery, resume work, applications, and follow-up into one record so a person can make decisions without reconstructing their search across tabs and inboxes. The product name is **Pathos**; P.A.T.H.O.S. is the expanded project name.

## The system, not a score

The public job board starts with source-linked postings. Importers normalize different employer career systems into one job record, preserve the source link, and avoid treating an interrupted check as proof that a role closed. Search and filters work without a resume. When a candidate provides enough context, “For you” can rank roles and show the evidence behind a match. Missing or weak evidence remains visible as uncertainty.

The signed-in product has four main destinations: Dashboard, Jobs, Tracker, and Profile. Pathos can help from those pages; resume optimization and coaching are focused actions rather than the entire navigation model. The tracker carries a role from saved through application, interview, and outcome, with its documents, status changes, and next steps attached.

## The resume is the source

A candidate can import or build a base resume in Resume Studio. For a particular role, the optimizer combines repeatable checks with model-assisted rewriting. The model can propose stronger wording or emphasis, but it does not get to invent a title, skill, credential, employer, or result. Source-aware validation checks the proposed document and restores or rejects unsupported claims. The final artifact is checked after cleanup so its reported analysis describes the version the candidate actually sees.

The score is an aid to inspecting a resume against a posting. It is not a claim to reproduce an employer's ATS or predict a hiring decision.

## The browser and inbox boundaries

The separately packaged Chrome extension detects job and application pages, prepares supported fields, attaches a reviewed resume for the role, and drafts supported screening answers from candidate evidence. It holds uncertain and sensitive fields for the person to review. Its application record is tied to observed submission intent, rather than treating a prepared form as a submitted job.

For email, the candidate chooses which messages to forward to a private Pathos address. The inbound handler authenticates the request, resolves the alias to its owner, looks for the right application, and classifies job-status evidence with rules before any bounded model fallback. A guarded result may update the tracker; uncertainty goes to review. The candidate can correct an applied result. The raw body is processed transiently rather than kept as a second mailbox.

## Architecture and trade-off

The web app uses React 19, React Router 7, Zustand 5, and Vite 8. Supabase provides authentication, Postgres with row-level security, storage, and Deno Edge Functions. Cloudflare Pages serves the web app; Workers run scheduled job ingest and related processing. Gemini is routed through server-side functions and subject to deterministic checks. Stripe handles billing. The extension is a separate Chrome Manifest V3 application.

The hard problem is keeping one claim consistent as it crosses those boundaries: a job must still point to its source, a resume change must still point to candidate evidence, an email update must still point to the right application, and a prepared application must not be mistaken for a submitted one. That is the organizing constraint behind the product.

Pathos is available at [yourpathos.app](https://yourpathos.app); the [source repository](https://github.com/thedevmark/pathosapp) documents its current architecture and product boundaries.
