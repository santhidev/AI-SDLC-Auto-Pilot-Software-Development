# Architecture / สถาปัตยกรรม

## EN
- **State**: `meta/sdlc-state.json` controls the pipeline.
- **Profiles**: lock decisions for stack, engineering, and design.
- **Artifacts**: SDLC documents are generated and become the truth.
- **Gates**: completion is PASS/FAIL based on objective criteria.
- **UI visibility**: previews are mandatory.
- **Evidence**: release artifacts are collected under `/evidence`.

## TH
- **State**: `meta/sdlc-state.json` คุม pipeline
- **Profiles**: ล็อกการตัดสินใจเรื่อง stack/engineering/design
- **Artifacts**: เอกสาร SDLC ถูก generate และกลายเป็นความจริง
- **Gates**: เสร็จหรือไม่เสร็จตัดสินด้วย PASS/FAIL
- **UI visibility**: ต้องมี preview เสมอ
- **Evidence**: หลักฐาน release เก็บใน `/evidence`
