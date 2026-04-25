# Stack Development Guidelines

## Features Documentation Maintenance

- Whenever a new feature is added, or an existing feature changes behavior/scope, update feature documentation in the same implementation cycle.
- Keep both documentation layers in sync under `Features/`:
  - Commercial/presentation: `features.es.md`, `features.en.md`, `features.pt_BR.md`
  - Technical/detail: `features-technical.es.md`, `features-technical.en.md`, `features-technical.pt_BR.md`
- While root-level legacy feature files in `Features/` still exist, keep them aligned too: `FUNCIONALIDADES_MEGA-ES.md`, `FUNCIONALIDADES_MEGA_EN.md`, `FUNCIONALIDADES_MEGA_PT_BR.md`.
- Do not close a feature documentation task until ES/EN/PT-BR are all updated and consistent.
- If structure or ownership changes, update `Features/README.md` in the same change.
