# analysis-test-environment
Docker files and descriptions on how to run interactive and batch analysis.  Useful as a
reference for developing and testing new analysis.


## Usage

### Preparing the repositories

1. Clone the internal-test-data into the data folder

   ``` bash
   git clone https://github.com/FASTGenomics/internal-test-data data
   ```

   Or supply your own test data, remember to use the proper FASTGenomics directory
   structure (e.g. `./data/dataset_0001/my_dataset.loom`) and provide a
   `dataset_info.json`.  Update the docker-compose file with the path to the data set
   (should point to a directory containing the `dataset_0001` folder in the example
   above).


1. Clone your favorite analysis into the `analysis` folder

   ``` bash
   git clone https://github.com/FASTGenomics/analysis_LIMES analysis
   ```

   You can use any other path on your local machine, just remember to update the
   corresponding `docker-compose.yml` path.

1. If you use an existing image specify it in the `docker-compose.yml`.

   Alternatively, if you want to develop and test an image clone it to the `image`
   folder (or any other format and update `docker-compose.yml`)

   ``` bash
   git clone https://github.com/FASTGenomics/image-jupyter-seurat image
   ```

   Note that in such case you'll have to run `docker-compose build`.


### Running the analysis

If you are developing an image you will need to re-build it every time you make some
changes to the images source code.  To do this run

``` bash
docker-compose build
```

To run an analysis in a batch-mode (non-interactive) simply run

``` bash
docker-compose up batch
```

This will generate an output file `analysis/analysis.html`.

To run an analysis in an interactive mode use

``` bash
docker-compose up interactive
```

This will start an [interactive jupyter under port 8886][session].

[session]: http://localhost:8886/lab/workspaces/analysis
