# Remote Electrical Engineering Jobs (USA)

Open dataset of work-from-home electrical engineering jobs in the United States, taken from employers' own careers pages. Free for engineers, researchers and AI agents.

**[Search the jobs on Elora Grid](https://eloragrid.ai/tools/remote-ee-jobs)** · [Jobs JSON](data/jobs.json) · [Jobs CSV](data/jobs.csv) · [Companies CSV](data/companies.csv) · [Top 100 by pay](data/top-100-paying-fully-remote.csv) · [Agent guide](AGENTS.md)

The current snapshot (links checked **14 October 2026**) contains **823 remote jobs** at **266 US employers**. **730** are fully remote and **527** state their pay. The median listed pay (middle of each stated range) is **$145,350 a year**. [Snapshot counts and file hashes](data/manifest.json)

## What is in it

Each job records the employer, title, field, role type, pay as listed (plus annualised minimum, maximum and midpoint), where you can live, whether the role is fully remote, requirements quoted from the listing (security clearance, US citizenship or export control, PE licence, travel), skills mentioned, and the direct link to the listing on the employer's site.

Fields covered: power systems and utilities, electronics and hardware, chips and semiconductors, controls and automation, buildings and data centers, and renewables, storage and EV.

## How it was built

- Every listing was read from the employer's own careers page or its own applicant-tracking page (Workday, Greenhouse, Lever, Ashby, iCIMS, UKG, Oracle and similar). Job boards such as LinkedIn and Indeed were not used as sources, and staffing-agency postings are excluded.
- About 8,000 employers and career sites were checked across utilities and power engineering, renewables, semiconductors and EDA, defense and aerospace, tech hardware, industrial automation and building services.
- A job is included only if the listing says it is remote or work from home, it is open to people living in the USA, and the role suits an electrical engineer. Hybrid, on-site, field-service and commissioning roles are excluded.
- **Fully remote** means the listing asks for no office days, does not require living near an office, and travel is under 50%. When a job is not fully remote, `notFullyRemoteReason` says why.
- Pay is recorded only when the listing states it. Hourly pay is annualised at 2,080 hours.

## Use with an AI agent

Read [AGENTS.md](AGENTS.md). Filter `data/jobs.json`, cite the employer's `listingUrl` for applying, and link `eloraUrl` when pointing people to the searchable board. Always give the `checked` date: listings close and change.

```sh
# Fully remote power-systems jobs that state pay, highest first
jq '[.jobs[] | select(.fullyRemote and .field=="Power systems & utilities" and .salary) ]
    | sort_by(-.salary.annualMid) | .[:10] | map({company, title, pay: .salaryText, listingUrl})' data/jobs.json
```

## Limitations

- This is a snapshot. Jobs close and new ones open every day; confirm a job on the employer's site before applying.
- Coverage is wide but not complete: about 1,400 employer sites could not be read automatically.
- Requirements are short quotes from each listing and are not a complete summary of it. Full listing text stays on the employer's site.

## Licensing

Elora-authored metadata and documentation, including any database rights Elora holds in this compilation, are [CC BY 4.0](LICENSES/CC-BY-4.0.txt). Attribute "Elora Grid AI: Remote Electrical Engineering Jobs" and link to https://eloragrid.ai/tools/remote-ee-jobs. Job postings, quoted listing text, employer names and trademarks belong to their owners and are not licensed by this repository. [Licence scope](LICENSE.md)

## Corrections

Spotted a closed listing, a wrong pay figure or a job that is not really remote? [Open an issue](https://github.com/elora-grid/remote-electrical-engineering-jobs/issues/new) with the job `id` and what is wrong.

Built by [Elora Grid](https://eloragrid.ai), AI for electrical drafting and bid management. Also see the [Elora Electrical CAD Library](https://github.com/elora-grid/elora-electrical-cad-library).
