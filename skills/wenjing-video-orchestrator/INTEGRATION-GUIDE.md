# Integration Guide

Install as top-level `wenjing-video-orchestrator`. Keep all eleven Independent Skills installed separately.

The orchestrator reads project `00_project_manifest.yaml` and `00_project_state.md`; it never imports downstream business modules. Independent Skills remain directly triggerable.

Supported content routes: `CASE`, `SOURCE_LOCKED`, `KNOWLEDGE`, `STORY`. All converge at valid `stage-outputs/03_script_LOCKED.md`; optional Reference Analysis may precede any route entry.

For v0.1, `DRY_RUN_GREEN` routes only to Producer DRY_RUN. Real production requires a new operator decision and real-media gates.
