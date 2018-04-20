.. _repository_overview:

*********************
Shyft Repositories
*********************
Shyft has a central concept of a `repository`. What is a `repository`? The idea is that these are classes that have
a well defined interface which can be seen at: `shyft/repository/interfaces.py`. These interfaces will interact with your
data (the persistence or data mapping layer) and the domain (in this case Shyft). The definition of a repository taken
from `Martin Fowler's blog <https://martinfowler.com/eaaCatalog/repository.html>`_ is:

    A Repository mediates between the domain and data mapping layers, acting like an in-memory domain object collection.
    Client objects construct query specifications declaratively and submit them to Repository for satisfaction.
    Objects can be added to and removed from the Repository, as they can from a simple collection of objects, and the
    mapping code encapsulated by the Repository will carry out the appropriate operations behind the scenes.
    Conceptually, a Repository encapsulates the set of objects persisted in a data store and the operations performed
    over them, providing a more object-oriented view of the persistence layer. Repository also supports the objective
    of achieving a clean separation and one-way dependency between the domain and data mapping layers.

In English please? Think of it this way, you have your data in your format. Shyft knows nothing about your format of
your data. You write a repository that provides the methods required according to the `interfaces.py` module. These methods
are guaranteed to return an object that Shyft understands (e.g. your data converted into a format suitable for Shyft).

This approach is greatly beneficial in that we don't require a data format for Shyft, but rather provide a mechanism for
you to 'connect' your data to Shyft. In this way, we can easily ingest operational data sources and forecasts such as
ECMWF data, meteorological forecasts, etc. If you have a model producing forecasts, you don't need to convert the output
data, you simply create a repository that knows how to prepare it for Shyft.

The `interfaces.py` module contains the abstract base-classes for the different
repositories in shyft, defining the methods that a repository should implement at a minimum.

According to architecture diagram/current code we do have repositories for::

    * region-model (`RegionModelRepository`)
                - for reading/providing the region-model, consisting of
                cell/catchment information, (typicall GIS system) for a given
                region/model spec.


    * state (`StateRepository`)
                - for reading region model-state, cell-level (snapshot of
                internal state variables of the models).

    * geo-located time-series (`GeoTsRepository`)
                - for input observations,forecasts, run-off time-series, that is
                useful/related to the region model. E.g. precipitation,
                temperature, radiation, wind-speed, relative humidity and even
                measured run-off, and other time-series that can be utilized
                by the region-model. Notice that this repository can serve
                most type of region-models.

    * interpolation parameters (`InterpolationParameterRepository`)
                - provides an encapsulation of the parameters required and
                methods

    * configuration
                - helps *orchestration* to assemble data (region, model,
                sources etc) and repository impl.

We try to design the interfaces, input types, return types, so that the number
of lines needed in the orchestration part of the code is kept to a minimum.

This implies that the input arguments to the repositories are types that goes
easily with the shyft.api. The returned types should also be shyft.api
compatible types, - thus the orchestrator can just pass on values returned into
the shyft.api.



Existing repositories
==============================

Recall, a repository is just a module or class that allows access to a collection of data in some arbitrary
format. In Shyft, it has the particular meaning of the **Python code** that can read this data and
feed it to the Shyft core.

The `shyft.repository` package includes the `interfaces` module which uses Python ABC
classes so that the user can provide concrete implementations of his/her
own repositories.  In this approach users can provide their own
repositories customized to their own configuration files (typically
slight variations of the YAML config files that come with Shyft) and a
diversity of data formats (maybe a whole collection of files,
databases, etc.).  In addition, some concrete repositories are being
distributed so that they can be used right away.  These concrete
repositories can also be taken as an example of implementation for
other user-defined repositories too.


