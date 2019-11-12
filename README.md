# analysis-test-environment

Docker files and descriptions on how to run interactive and batch analysis.  Useful as a
reference for developing and testing new analysis.

## Usage

### Preparing the repositories

1. Clone the [test-data](https://github.com/FASTGenomics/test-data) into a newly created data folder within this repository

   ``` bash
   git clone https://github.com/FASTGenomics/test-data data
   ```

   Alternatively, supply your own test data - but remember to use the proper FASTGenomics directory
   structure (e.g. `./data/dataset_0001/my_dataset.loom`) and provide a
   `dataset_info.json`.  Update the docker-compose file with the path to the data set
   (should point to a directory containing the `dataset_0001` folder in the example
   above).

1. Clone your favorite analysis (`analysis.ipynb`) into the `analysis` folder, e.g.,

   ``` bash
   git clone https://github.com/FASTGenomics/analysis_scanpy_pbmc3k analysis
   ```

   You can use any other path on your local machine, just remember to update the
   corresponding `docker-compose.yml` path. All the data in the analysis folder will be available in your analysis.
   Our available analyses can be found [here](https://github.com/search?q=topic%3Afastgenomics-analysis+org%3AFASTGenomics&type=Repositories)

1. If you use an existing image specify it in the `docker-compose.yml`.

   Alternatively, if you want to develop and test an image - clone it to the `image`
   folder (or any other format and update `docker-compose.yml`)

   ``` bash
   git clone https://github.com/FASTGenomics/image-jupyter-scanpy image
   ```

   and uncomment the `build: ...` option in `docker-compose.yml`.
   
   The latest versions of our standard images (`fastgenomics/jupyter-scanpy` and `fastgenomics/jupyter-seurat`) can be found
   on [dockerhub](https://hub.docker.com/u/fastgenomics).
   
   If you want to develop your own images make sure to always use the latest `fastgenomics/jupyter-base` version as a strating point.

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
