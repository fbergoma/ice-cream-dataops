# ice-cream-dataops

Cognite Data Fusion Bootcamp data foundation, following the PDFs in this order:

1. Introduction
2. Data Sources & Use Cases
3. Create Azure Service Principal (already completed externally)
4. Setup the CDF Toolkit
5. CDF Toolkit Modules

Toolkit is pinned to `0.6.53`. The starter function source files are copied from
that release's Bootcamp package. The root `cdf.toml` points to the nested
`ice-cream-dataops/` organization directory created by the Bootcamp initializer.
Run all commands from the repository root.

Fill in the placeholders in `.env` using your **test** project, existing application
client IDs, secret **values**, and group object IDs. `.env` is ignored by Git.
Also set `environment.project`
in `ice-cream-dataops/config.test.yaml` to the same project as `CDF_PROJECT`.
Production configuration is a later bootcamp exercise and is not included here.

Rebuild the Codespace container to use the PDF's Python 3.11 and Poetry setup,
then install the dependencies:

```bash
poetry install
```

The PDF also requires a CDF group named `cognite_toolkit_service_principal`, with
Project and Group capabilities and the admin-tk Entra group's object ID as its
source ID. If this CDF-side bootstrap step is still pending, complete it in the CDF
Admin workspace before verifying authentication. No Entra resources are created
by this repository.

After filling in the configuration, verify, build, and inspect the deployment:

```bash
poetry run cdf auth verify
poetry run cdf build
poetry run cdf deploy --dry-run
```

When the dry run succeeds, deploy:

```bash
poetry run cdf deploy
```

The configuration creates the `data_developer`, `icapi_extractors`, and
`data_pipeline_oee` groups; the `ds_icapi` and `ds_uc_oee` datasets; the
`ice-cream-factory-db` RAW database with its `assets` table; and the
`icapi_dm_space` and `oee_ts_space` spaces. Group capabilities follow the PDF's
YAML examples. Although its introduction mentions a second extractor state table,
the PDF defines only `assets`, and the bundled extractor does not use a RAW state
table, so no additional table is invented here.

The bundled Python functions are starter code for later exercises; these PDFs do
not define function deployment YAML, schedules, or extraction pipelines.
No remote authentication or deployment is performed while secrets are placeholders.
After deployment, check group source IDs, datasets, RAW, and spaces in Fusion as
described in the final PDF, then commit and sync when ready.
