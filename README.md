# DSC Setup

Sets up a new conservancy's EarthRanger site for Distance Sampling Count (DSC) surveys. It creates whatever the site
is missing from the shared DSC schema, then checks the site and shows what's left to do.

## What it does

1. **Creates the missing items** on the chosen conservancy:
   - an event category, only if the site has none;
   - the `Distance Count` patrol type;
   - the `Distance Count Patrol MetaData` and `Distance Count Wildlife Sighting` event types, with their fields and
     form layouts;
   - the empty `DSC_Transects` feature group.

   It only creates items. Anything that already exists is left as it is, and listed if it differs from the schema.
2. **Checks the site** against the shared DSC schema, the same check as *DSC Onboarding Check*.
3. **Shows a dashboard:**
   - tiles for items created, still to create, checks failed, warnings and checks passing;
   - the onboarding progress;
   - what to do next;
   - the two IDs DSC Analysis needs;
   - the checklist;
   - a map of the transects.

Not created here, so add them in EarthRanger after the run:
- **Species:** the `distancecountwildlife_species` choice list.
- **Team members:** the `distancecountpatrol_teammembers` choice list.
- **Transect features and transect choices:** added once the transects are final.

> **This version creates straight away.** *Create the missing items* is fixed on in `spec.yaml`, so there is no
> preview run. To see what would be created without changing the site, run *DSC Onboarding Check* first.

## Requirements

- An **EarthRanger** connection for the conservancy being set up. The account needs permission to add patrol types,
  event types and feature groups.
- Optionally, a connection for a **template conservancy** (read-only access is enough).

---

## 1. Load the Workflow

In the workflow runner, add a new template using this repository's URL. Once added, select
**DSC Setup** from the available templates list to load it.

---

## 2. Configure the Workflow

### Conservancy

| Field | Description | Default |
|---|---|---|
| Data source *(required)* | The conservancy to set up. | — |

### DSC Setup

| Field | Description | Default |
|---|---|---|
| Template conservancy | The conservancy whose look the new setup copies (see below). | Empty: Enarau's look |

### Set Workflow Details

| Field | Description | Default |
|---|---|---|
| Workflow Name *(required)* | A name for this run. | — |

### Template conservancy

A template only sets how the new setup **looks**:
- the event types' form layouts;
- field titles and descriptions;
- icons, priorities and geometry.

The fields themselves always come from the shared schema: keys, types, required flags, choice lists, limits and event
type values. So the new site passes the check whichever template is picked. The template site is only read.

- **Left empty:** Enarau's look, from the copy in the task package.
- **A form that uses other field names:** that form falls back to Enarau's layout, for example Enonkishu's MetaData
  form, which uses `Transect_ID`, `Team_members` and `Number_of_observers`. Titles and icons still come from the
  template.
- **A template without a DSC setup:** the missing parts fall back to Enarau's.

The *Template* row of the setup table says which template was used and what fell back.

---

## 3. After the run

1. Follow **What to Do Next** on the dashboard.
2. Add species and team members to their choice lists in EarthRanger.
3. Run the workflow again. Only what's still missing is created, and the checklist updates.
4. Copy the IDs under **For DSC Analysis** into DSC Analysis.

---

## Developing

```bash
# recompile spec.yaml (first time: --install; after that: --update, which bumps VERSION.yaml)
./dev/recompile.sh --update

# run the test cases in test-cases.yaml
pixi run --manifest-path pixi.toml -e default bash dev/pytest-cli.sh dsc_setup --all
```

The tasks come from `ecoscope-workflows-ext-distance-sample-counts` (`tasks/onboarding/`), in the
`workflows/distance_sample_counts` repo. Changes to what is created or checked are made there, not in this spec.

Documentation: [docs/index.html](docs/index.html).
