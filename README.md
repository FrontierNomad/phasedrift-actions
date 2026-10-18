# PhaseDrift baseline collector

A pinned reusable workflow for measuring the exact default-branch revision of an account-connected repository. It uploads compact metric results and provenance to PhaseDrift. Source files, raw reports and transcripts are not uploaded.

Follow [the setup guide](https://phasedrift.ai/docs/github-baselines). Your setup agent runs `phasedrift baseline connect`, reviews runner availability and generates the caller with `phasedrift baseline workflow`. Pin this workflow to a reviewed full commit SHA. No laptop credentials or PhaseDrift secrets belong in the caller.

The workflow defaults to an explicitly approved self-hosted runner with `self-hosted` and `phasedrift-baseline` labels. Installation alone does not provision a runner. Private caller hosted minutes can incur charges. Unrelated Actions, backups and paid analysis are unchanged.

Supported collectors: Linux x64 and macOS ARM64. Git, Node.js and Perl are required. The collector includes a pinned runtime and analyzers. The current workflow runs structural diagnostics; it does not run project builds, tests or deployments.

The collector is PhaseDrift subscription software. This repository contains only its workflow orchestration and documentation. Report security issues privately to hello@phasedrift.ai.
