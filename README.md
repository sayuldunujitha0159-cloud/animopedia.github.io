# ANIMOPEDIA

ANIMOPEDIA is a global animal encyclopedia and digital natural-history museum.

## Implemented product foundation

- Age-private onboarding with country personalization and global browsing
- Structured starter animal records and evidence/source labels
- Animal search, collections, favorites, habitats, country context, conservation, extinction, and evolution surfaces
- ANI and OWL PROFESSOR learning entry points
- Accessible responsive UI and local settings
- Offline-first shell with a service worker, manifest, online/offline status, and cached application resources

## Part 5 production architecture

The frontend deliberately does **not** pretend to provide server-backed capabilities that are not present. The following boundaries are explicit for the next implementation phase:

- **Daily verified updates:** publish only records in `approved`/`published` state; if no verified candidate exists, delay publication rather than fabricate a discovery.
- **Review workflow:** `draft → under_review → needs_revision | rejected → approved → published`, with immutable update history and source/date metadata.
- **Admin security:** admin operations must be server-side, authenticated, authorized, rate-limited, and protected from frontend-only permissions. Never place API keys in this client.
- **ANI security and cost:** retrieve only relevant approved records, treat external text as untrusted data, cache safe answers, and enforce request limits on a protected server endpoint.
- **Sync:** use version/checksum checks, transactional local writes, conflict records, retries, and rollback; never report synchronization success when it fails.
- **Provenance:** photographs, audio, fossil specimens, reconstructions, and illustrations require source, creator, license, attribution, and media-type labels before publication.
- **Reports:** user reports enter an administrative queue and never mutate scientific records automatically.

## Local development

```bash
npm install
npm run dev
```

The service worker is active in a production build/served deployment. Browser storage currently holds onboarding and favorites locally; account synchronization, server review, notifications, and licensed media require a backend and must be added without weakening these safeguards.
