# Quality Gates

## Universal

- [ ] Working `.mdj` exists if required.
- [ ] PNGs exist and are readable.
- [ ] Manifest covers every PNG.
- [ ] Source `.mdj` was not modified directly.
- [ ] Engineering verification passed.
- [ ] Visual quality verification passed.
- [ ] Source preservation verification passed when a source model exists.

## Diagram Gates

- [ ] Use case:
- [ ] Class:
- [ ] Sequence:
- [ ] Activity:
- [ ] Communication:
- [ ] State:
- [ ] Component:
- [ ] Deployment:

## Status

- `Verified | Unverified: <reason> | Failed: <reason>`

## Split Status

- engineeringStatus:
- visualStatus:
- sourcePreservationStatus:

Do not mark final `Verified` unless all applicable split statuses are `Verified`.
