# Damavand

<p align="center">
  <img src="docs/assets/images/logo_new_cropped.jpg" alt="Damavand Logo" width="300">
</p>

This repository hosts the official documentation of Damavand; a package to simplify rotary machines vibration-based analysis, through standardizing downloading, loading and transforming processes. Checkout the following link to land on the documentation website:

[https://pydamavand.github.io/documentation/](https://pydamavand.github.io/documentation/)

You can also find the package repository at the following link:

[https://github.com/pydamavand/damavand](https://github.com/pydamavand/damavand)

## Installation

Currently, Damavand is accessible through the official Github repository, as below:

```bash
git clone https://github.com/pydamavand/damavand
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

## Licence

Damavand is dual-licensed: free for non-commercial use under the
[PolyForm Noncommercial License 1.0.0](LICENSES/NONCOMMERCIAL.txt).

Use within a commercial product or for internal business operations in a for-profit organization requires a separate commercial license. Please contact [ahberenji@gmail.com](mailto:ahberenji@gmail.com) for inquiries.  

See [LICENSES/LICENSE.md](LICENSES/LICENSE.md) for full details.


## Cite
