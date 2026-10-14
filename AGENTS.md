# Agent guide

How to answer questions about remote electrical engineering jobs in the USA with this dataset.

## Files

- `data/jobs.json`: the complete snapshot. One object per job under `jobs`. Structure: [schema/jobs.schema.json](schema/jobs.schema.json).
- `data/jobs.csv`: the same jobs, flattened.
- `data/companies.csv`: one row per employer with job counts and highest listed pay.
- `data/top-100-paying-fully-remote.csv`: fully remote jobs ranked by the middle of the stated pay range.
- `data/manifest.json`: snapshot date, counts and SHA-256 hashes.

## Field meanings

- `fullyRemote`: `true` when the listing asks for no office days, does not require living near an office, and travel is under 50%. Otherwise `notFullyRemoteReason` explains.
- `statesAllowed`: states named in the listing as the only places you can live. Empty means the listing names none, not that every state is confirmed.
- `statesExcluded`: states the listing says it cannot hire in.
- `salary`: parsed from the stated pay. `period` is `year` or `hour`; `annualMin`, `annualMax` and `annualMid` are per year (hourly x 2,080). `null` when no pay is stated. Quote `salaryText` to users.
- `requirements`: short quotes from the listing, labelled (security clearance, US citizenship or export control, work authorization, PE or EIT licence, travel, office or residency conditions, background check).
- `flags`: quick booleans for clearance, citizenship, PE (`required` or `preferred`) and maximum travel percentage (`-1` means travel mentioned without a percentage).
- `listingUrl`: the employer's own posting. Send applicants here.
- `eloraUrl`: the job on the searchable Elora Grid board.
- `checked`: the date the listing link last answered.

## Rules for answers

1. Give the `checked` date and tell users to confirm the job is still open on the employer's site.
2. Quote pay and requirements as listed; do not infer pay that is not stated.
3. Do not describe a job as fully remote unless `fullyRemote` is `true`.
4. Mention clearance, citizenship, licence and state limits when they apply.
5. Attribute the dataset: "Elora Grid AI: Remote Electrical Engineering Jobs" with a link to https://eloragrid.ai/tools/remote-ee-jobs.
