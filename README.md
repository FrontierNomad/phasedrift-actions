# PhaseDrift baseline collector

A pinned reusable workflow for measuring the exact default-branch revision of an account-connected repository. It uploads compact metric results and provenance to PhaseDrift. Source files, raw reports and transcripts are not uploaded.

Follow [the setup guide](https://phasedrift.ai/docs/github-baselines). Your setup agent runs `phasedrift baseline connect`, reviews runner availability and generates the caller with `phasedrift baseline workflow`. Pin this workflow to a reviewed full commit SHA. No laptop credentials or PhaseDrift secrets belong in the caller.

The workflow defaults to an explicitly approved self-hosted runner with `self-hosted` and `phasedrift-baseline` labels. Installation alone does not provision a runner. Private caller hosted minutes can incur charges. Unrelated Actions, backups and paid analysis are unchanged.

Supported collectors: Linux x64 and macOS ARM64. Git, Node.js and Perl are required. The collector includes Bun 1.4.3 and pinned analyzers. Each job verifies both embedded runtimes and logs the immutable build metadata before scanning. The current workflow runs structural diagnostics; it does not run project builds, tests or deployments.

The collector is PhaseDrift subscription software. This repository contains only its workflow orchestration and documentation. Report security issues privately to hello@phasedrift.ai.

## Collector updates

Archives and workflow commits are immutable. Existing callers keep their reviewed version until upgraded deliberately. When upgrading, let active baseline jobs finish, re-run `phasedrift baseline connect` to authorize the current server-approved workflow using the existing App installation, then generate `phasedrift baseline workflow` and review its exact SHA. Merge only that caller change through the repository release process. Do not broaden App permissions or enable unrelated workflows.

Accept the upgrade only after a genuine main push reports the new build/runtime in GitHub logs and `phasedrift baseline status` agrees on the exact main commit and acknowledged attempt. Repeating the frozen upload must return the same receipt. A runtime change creates a new environment comparison group; older results remain historical evidence.

## Recovery and admission

Collector 0.4.46 checks admission before scanning, retries transient failures at most three times per operation, and reuses the exact frozen payload for upload retries. Permanent capacity and authorization failures stop. Ordinary baselines scan once. Set `exercise-lost-ack: true` only for a targeted integration run to replay an acknowledged payload without rescanning.

After a failed job, only compact `upload.json` is retained as a one-day artifact; temporary analyzer files are removed. Recovery remains bound to the same genuine run and attempt within 24 hours. A new workflow attempt cannot upload a previous attempt's payload.
