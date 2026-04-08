# WormWideWeb-data
## Adding a new paper/project
### paper_id
Pick a unique `paper_id` e.g. `atanas_kim_2023` and `dag_nwabudike_kang_2023`

### Paper data
Add an entry in `activity/papers.json` e.g.:
```json
{
  "paper_id": "atanas_kim_2023",
  "title_full": "Brain-wide representations of behavior spanning multiple timescales and states in C. elegans",
  "title_short": "Atanas & Kim et al., 2023",
  "neuropal_label": true,
  "encoding_data": true,
  "repository": {
    "type": "zenodo",
    "record_id": "19388374"
  }
}
```
- paper_id: unique paper id
- title_full: full title
- neuropal_label: true or false. if true, neorpal label must be in the repository
- encoding_data: true or false. if true, encoding data files must be in the repository
- repository: repository info. type: zenodo or dryad. record_id: use the record id for zenodo, the doi for dryad

### Dataset types data
Add dataset types information entry for the paper, using the same `paper_id`. Commonly used data types such as `neuropal` don't need to be added.

Add the entry in `activity/dataset_types.json` e.g.:
```json
{
  "atanas_kim_2023": [
    {
      "id": "baseline",
      "name": "Baseline",
      "color_background": "rgb(125,125,125)",
      "description": "Baseline dataset"
    },
    {
      "id": "heat",
      "name": "Heat",
      "color_background": "#dc3545",
      "description": "Heat stimulation experiment data"
    },
    {
      "id": "gfp",
      "name": "GFP",
      "color_background": "#198754",
      "description": "Control data with the GFP expression strain"
    }
  ]
}
```

### Manifest
If already not there, create a csv file using the matching paper_id in `activity/raw`.
The csv file should contain the following columns:
- filename: h5 file name
- checksum: sha256 checksum of the h5 file
- uid: unique id for the dataset
- θh_pos_is_ventral: true if positive/+ θh is ventral
- label: true if there's neuropal data
- type: dataset types from the dataset_types.json comma separated. e.g.: "baseline,neuropal"
- event: events e.g. "stim_begin_confocal=[300,600],food_encounter=[100]"
- t_range: time point range to display on the web app. e.g. skip if you want the full dataset. otherwise, specify as start:end e.g. "601:800"

### Repository
Each zenodo or dryad repository must contain:
- processed_h5.tar.bz2: archive of h5 files

If the paper has encoding data (ouputs of `generate_encoding_files` in `WormWideWebData.jl`):
- neuron_categorization.h5.bz2
- encoding_changes_corrected.h5.bz2
- relative_encoding_strength_median.h5.bz2
- tuning_strength.h5.bz2
- sampled_tau_vals_median.h5.bz2
- fit_ranges.h5.bz2

If the paper has NeuroPAL labels (ouput of `generate_neuropal_json` in `WormWideWebData.jl`): 
- neuropal_label.json.bz2