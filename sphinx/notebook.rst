The following notebooks are available in the `shyft-doc <https://github.com/statkraft/shyft-doc>`_ repository.
You can download and run these on your local computer, or browse through them here.

.. _api-introduction:

An introduction to the `api`
------------------------------------
It is recommended to go through these simple notebooks first, just to get a sense of the Shyft :class:`api`

.. toctree::
    :maxdepth: 1

    notebooks/api/api-intro
    notebooks/api/single_cell

.. _config-introduction:

Getting started with configured simulations
---------------------------------------------
Once you've completed that, take a look at the configured examples. These use `yaml` files to keep model
configuration data, and are a good starting point for understanding how to set up a Shyft simulation with your
own data.

.. toctree::
    :maxdepth: 1

    notebooks/nea-example/simulation-configured
    notebooks/nea-example/calibration-configured

.. _advanced_tools:

Some more advanced tools within Shyft
--------------------------------------------
Shyft contains a lot of functionality. A few pieces are shown in the following notebooks.

.. toctree::
    :maxdepth: 1

    notebooks/api/api-timeseries
    notebooks/api/api-ts-partition_by_and_percentiles
    notebooks/api/api-ts-convolve
    notebooks/repository/repositories-intro
    notebooks/grid-pp/gridpp_geopoints
    notebooks/grid-pp/gridpp_simple
