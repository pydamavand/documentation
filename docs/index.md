# Damavand

<p align="center">
  <img src="/assets/images/logo_new_cropped.jpg" alt="Damavand Logo" width="300">
</p>

## Introduction

Damavand is a package to simplify rotary machines vibration-based analysis, through standardizing downloading, loading and transforming processes. The main motivation behind developing it is to democratize rotary machine intelligent predictive maintenance, through the development of an end-to-end unified data processing framework, covering from downloading the raw data to data preprocessing.

## Installation

Currently, Damavand is accessible through the official Github repository, as below:

```bash
git clone https://github.com/amirberenji1995/damavand
```

Once the repository is cloned, install the dependencies as below:

```bash
pip install -r damavand/requirements.txt
```

## Quickstart

Once the package is installed, its whole functionality is accessible; the code snippet below, demonstrate a simple usage scenario, where a dataset is downloaded, loaded and processed.

```Python
# Importings
from damavand.damavand.datasets.downloaders import read_addresses, ZipDatasetDownloader
from damavand.damavand.datasets.digestors import UoO
import pandas as pd

# Downloading the dataset
addresses = read_addresses() # reading the addresses
downloader = ZipDatasetDownloader(addresses['UoO']) # instantiating the downloader to download the UoO dataset (https://data.mendeley.com/datasets/v43hmbwxpm/1)
downloader.download_extract('UoO.zip', 'UoO/')  # downloading and extracting the dataset

# Mining the dataset
dataset = UoO('UoO/', ['Channel_1', 'Channel_2'], [1]) # instantiating the dataset
mining_params = {'win_len': 10000, 'hop_len': 10000} # defining the mining parameters
dataset.mine(mining_params) # mining the dataset

# Aggregating the mined data over the first channel
df = pd.concat(dataset.data['Channel_1']).reset_index(drop = True)

# Signal/Metadata split
signals, metadata = df.iloc[:, : -3], df.iloc[:, -3 :] # last three columns are state, loading and repetition; therefore, they are excluded into metadata
```

## Documentation

Detailed API reference of each module is accessible through the links, below:

- [**Datasets**](datasets.md)
- [**Signal Processing**](signal_processing.md)
- [**Augmentations**](augmentations.md)
- [**Utilities**](utils.md)

## Demonstrations and Tutorials

For each dataset available in this package, a detailed demonstration is provided that includes downloading, mining and time-domain visualization. These demonstrations can be found [here](https://github.com/amirberenji1995/damavand/tree/main/dataset_demonstrations).

Additionally, following tutorials are provided:

1. [Signal Processing 101](notebooks/tutorials/signal_processing_101.ipynb)
2. [How to develop a digestor for a custom dataset?](notebooks/tutorials/custom_digestor_development.ipynb)
3. [How to develop a custom feature to extract?](notebooks/tutorials/custom_feature_extraction.ipynb)
4. Anomaly detection (Comming soon!)
5. [Health state classification](notebooks/tutorials/Classification_demo.ipynb)

## License

Damavand is dual-licensed: free for non-commercial use under the
[PolyForm Noncommercial License 1.0.0]().

Use within a commercial product or for internal business operations in a for-profit organization requires a separate commercial license. Please contact [ahberenji@gmail.com](mailto:ahberenji@gmail.com) for inquiries.  

See [LICENSES/LICENSE.md]() for full details.


## Next steps

We highly encourage other developers to help in extending the Damavand, particularly in the following directions:

1. Adding new datasets
2. Adding new signal processing methods


## Cite

