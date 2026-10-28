# Dsc setup

Dsc setup

## What it does

| Step | What it does |
|---|---|
| **Connect to EarthRanger** |  |
| **Set Up DSC** | Create the Distance Sampling Count setup an EarthRanger site is missing: an event category (if the site has none), the Distance Count patrol type, both event types with their fields and form layouts, the transect choices and the DSC_Transects feature group. Species and team members aren't created; they are set up in EarthRanger. |
| **Count Items Still to Create** | The number of rows whose status is one of `statuses`, e.g. the checks that failed. Rows that describe the run (Site, Run, IDs) have status Info, so they're only counted when Info is asked for. |
| **Fetch Transects** | The site's DSC_Transects features (name and geometry, EPSG:4326), read-only. Empty when there is no group or it has no features yet. |
| **Persist Setup Table** | Persist dataframe to a file or cloud storage object. |
| **Count Created Items** | The number of rows whose status is one of `statuses`, e.g. the checks that failed. Rows that describe the run (Site, Run, IDs) have status Info, so they're only counted when Info is asked for. |
| **Still to Create Widget** | Create a single value widget with a single view. |
| **Check DSC Setup** | Check that an EarthRanger site has the Distance Sampling Count setup new conservancies need: the Distance Count patrol type, both event types and their fields, the species and transect choice lists, and the DSC_Transects feature group with one correctly named transect per choice. Read-only. |
| **Transect Labels** | One point per transect, on the line, with its name in a `label` column, for a text layer. |
| **Transect Map View** | A map view framing the transects. Takes the transects directly, not in a list, so the step can be skipped when there are none. |
| **Transect Lines Layer** | Creates a GeoJSON layer definition based on the provided configuration. |
| **Persist Checklist** | Persist dataframe to a file or cloud storage object. |
| **Transect Names Layer** | Creates a text layer definition based on the provided configuration. |
| **Draw Onboarding Progress** | An HTML card showing where the site is in DSC onboarding: one step per stage, ticked when its checks pass, with the current step highlighted. Sites surveyed before the rules show their differences in amber. |
| **Next Steps** | Markdown: what this run did, then one plain instruction per failed check (and warnings worth a look), or the next step when nothing is left to fix. |
| **Format Checklist** | The checklist for reading: grouped by area, failures first within each, with a symbol on each status and, when the setup table is given, a This run column (Created, Would create, Already there, …). |
| **Count Failed Checks** | The number of rows whose status is one of `statuses`, e.g. the checks that failed. Rows that describe the run (Site, Run, IDs) have status Info, so they're only counted when Info is asked for. |
| **Count Warnings** | The number of rows whose status is one of `statuses`, e.g. the checks that failed. Rows that describe the run (Site, Run, IDs) have status Info, so they're only counted when Info is asked for. |
| **Checks Passing** | The share of checks that don't fail, out of those that pass, warn or fail (information isn't counted). |
| **Analysis IDs** | Markdown: the two IDs DSC Analysis needs for this site, ready to copy. |
| **Base Maps** |  |
| **Draw Transect Map** | Creates a map based on the provided layer definitions and configuration. |
| **Persist Onboarding Progress** | Persist text to a file or cloud storage object. |
| **Next Steps Widget** | Create a text widget with a single view. |
| **Draw Checklist Table** | Creates an HTML table of the dataframe, like draw_table, with rows coloured by a status column. |
| **Analysis IDs Widget** | Create a text widget with a single view. |
| **Persist Checklist Table HTML** | Persist text to a file or cloud storage object. |
| **Onboarding Progress Widget** | Create a table widget with a single view. |
| **Created Widget** | Create a single value widget with a single view. |
| **Warnings Widget** | Create a single value widget with a single view. |
| **Persist Transect Map** | Persist text to a file or cloud storage object. |
| **Checklist Widget** | Create a table widget with a single view. |
| **Failed Checks Widget** | Create a single value widget with a single view. |
| **Checks Passing Widget** | Create a single value widget with a single view. |
| **Set Workflow Details** | Add information that will help to differentiate this workflow from another. |
| **Transect Map Widget** | Create a map widget with a single view. |
| **Gather Dashboard** |  |

## Requirements

- Access to a **EarthRanger** data source, set up as a connection

---

## 1. Load the Workflow

In the workflow runner, add a new template using this repository's URL. Once added, select
**Dsc setup** from the available templates list to load it.

---

## 2. Configure the Workflow

You'll be prompted to fill in the following parameters before running.

### Connect to EarthRanger

| Field | Description | Default |
|---|---|---|
| Data source *(required)* | Select one of your configured data sources. | — |

### Set Up DSC

| Field | Description | Default |
|---|---|---|
| Template conservancy | The conservancy whose form layouts, field titles and icons the new setup copies. The fields and event types themselves are always the shared DSC schema. Leave empty to use Enarau's. | — |

### Set Workflow Details

| Field | Description | Default |
|---|---|---|
| Workflow Name *(required)* |  | — |

---

## Developing

```bash
# recompile spec.yaml (first time: --install; after that: --update, which bumps VERSION.yaml)
./dev/recompile.sh --update

# run the test cases in test-cases.yaml
pixi run --manifest-path pixi.toml -e default bash dev/pytest-cli.sh dsc_setup --all
```

Documentation: [docs/index.html](docs/index.html).
