# ANIMOPEDIA data and review contract

This document defines the server-side contract before production scientific data is connected.

## Record metadata

Each animal/update must include: stable ID, created timestamp, updated timestamp, last verified timestamp, taxonomic version, evidence state, confidence, source IDs, distribution precision, and media provenance.

## Publication states

`draft`, `under_review`, `needs_revision`, `rejected`, `approved`, and `published`. Only `published` records are eligible for public daily discovery or offline package generation.

## Update history

Store append-only events with actor, timestamp, previous version, next version, reason, source references, and rollback target. A failed import remains visible as `failed_import` and is never silently published.

## Offline packages

Packages are versioned manifests containing approved JSON records, quiz/museum content, licensing metadata, byte size, checksum, and an expiry/review date. Use IndexedDB transactions for download/install and retain the last known-good package on failure.

## User reports

Reports contain record ID, category (`facts`, `photo`, `source`, `taxonomy`, `distribution`, `other`), user description, created time, and review status. Reports do not directly edit records.

## QA gates

Before release, test onboarding and privacy, global country access, search/filter behavior, source and distribution wording, keyboard/screen-reader flows, offline startup and recovery, synchronization failure rollback, admin authorization, ANI retrieval boundaries, mobile performance, and media license/provenance checks.
