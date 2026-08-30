# Hands-on CDSE

Materials from **Hands-on CDSE: From Copernicus Browser to Evalscripts and APIs**,
a three-hour workshop at FOSS4G 2026 in Hiroshima.

Everything here runs on the Copernicus Data Space Ecosystem **free tier**. No contract,
no quota upgrade, no institutional account.

## What's here

| File | What it is |
|---|---|
| [`hands-on-cdse.pdf`](hands-on-cdse.pdf) | The full deck |
| [`notebook.ipynb`](notebook.ipynb) | Jupyter notebook: auth, Process API, Statistical API, a ten-lake time series |
| [`clms-collection-list.md`](clms-collection-list.md) | Every global CLMS collection with its id, band tables and documentation link |
| [`papers.md`](papers.md) | 54 published methods you could implement, with DOIs. Formulas deliberately left out |

## Running the notebook

```bash
pip install sentinelhub matplotlib
```

You need a free CDSE account (register at [dataspace.copernicus.eu](https://dataspace.copernicus.eu))
and an OAuth client.

To create the client: open the Copernicus Browser, click **SH DASHBOARD** at the top of the
left-hand panel, then **User settings → OAuth clients → Create**. The client secret is shown
**once** and cannot be retrieved after you close the dialog, so copy it before you do.

Put the credentials in `~/.config/sentinelhub/config.toml`, or paste them into the first cell.
Don't commit them.

## The collection list

`clms-collection-list.md` is the useful one months later. It carries `Type`,
`Raw range`, `Scaling` and `Offset` for every band, which is what stops an AI inventing a
plausible-looking scale factor for a product it has never seen.

Three things in there that catch people out:

- **`clms_global_` is a namespace, not a coverage claim.** Some products are Europe-only.
- **`RT` is the consolidation period.** Each level is a separate collection id, and there is
  no automatic fallback between them.
- **A Browser id is not a CDSE STAC id.** The same product is named differently in each.

## Writing evalscripts

The official CDSE collection is
[eu-cdse/sentinel-hub-custom-scripts](https://github.com/eu-cdse/sentinel-hub-custom-scripts)
— 485 scripts, GPL-3.0, one folder per product. Read three before you write one.

[`papers.md`](papers.md) is the "implement a paper" menu: 54 published, open-access methods
that work on CDSE data, grouped by theme, each with a DOI. **The formulas are not in there on
purpose** — deriving one from the paper is the exercise, and every entry is one click from the
real thing.

To browse rather than choose,
[awesome-spectral-indices](https://github.com/awesome-spectral-indices) lists 280 indices with
formulas, bands and DOIs. They are third-party transcriptions, so follow the DOI when it
matters.

## Useful links

- Documentation — <https://documentation.dataspace.copernicus.eu>
- Forum, where the team and other users answer — <https://forum.dataspace.copernicus.eu>
- Requests Builder, a GUI that exports runnable Python — <https://shapps.dataspace.copernicus.eu/requests-builder>
- Sentinel Hub dashboard — <https://shapps.dataspace.copernicus.eu/dashboard>

## Credits

Imagery throughout: contains modified Copernicus Sentinel data and Copernicus Service
information.

Workshop by Klemen Lovenjak, Sinergise.
