# Choroscope

## What is Choroscope?

Choroscope is a visualization platform for geospatial data. Created to showcase results for the [Local Burden of Disease (LBD)](http://www.healthdata.org/lbd) project at the [Institute for Health Metrics and Evaluation (IHME)](http://www.healthdata.org), Choroscope provides a flexible format for exploring and sharing data linked to geography.

## What does the name mean?

"Choroscope" is a synthetic word derived from the Greek χώρα (_chora_), "place," and σκoπέω (_skopeo_) "to look at, contemplate, or examine." Choroscope is about studying data as distributed over geography.

## How does Choroscope work?

The platform ingests a geospatial data set with an accompanying configuration file specifying the shape of the data and details of how it should be displayed. A database creation tool, `choroscope-db`, builds a geospatial database from the data, and an application server, `choroscope-api`, makes it available as a web API. A frontend web application, `choroscope-app`, uses this API to display both choropleths and highly detailed image-like maps - for which pixel colorization is done in the browser with a custom WebGL renderer. The configuration language, defined in `choroscope-spec`, allows the addition of other visualizations, like line and bar graphs, to supplement the primary map-based view.

## How did Choroscope come to be?

Choroscope grew out of the Local Burden of Disease (LBD) project at IHME, and its features and design strongly reflect the needs of that project. Above all, LBD needed a flexible and open-ended tool to visualize a large number of data sets of differing shapes and with differing needs. As of this writing, the LBD application is being used to visualize population health estimates accompanying eight scientific publications, with many more in the works. Because of the tool's flexibility, we the developers of the software came to realize that the underlying platform could, in principle, be used to visualize _any_ compatible data set - it wasn't limited to LBD estimates or even health data. In the spirit of open sharing of information embraced by LBD, IHME, and the scientific community generally, we wanted to offer the core platform as open-source software so that others could use it to visualize their geospatial data sets, ultimately helping us all to better understand our world.

## How can I use Choroscope to visualize my own geospatial data set?

You can't just yet, but as the platform is published, we plan to provide reference documentation, tutorials, and demos to help you set it up to serve your own needs.

## What are the components of the Choroscope platform, and what is the plan for publishing them?

The plan is to publish the individual components of Choroscope in sequence, proceding conceptually from bottom to top:

- [`choroscope-spec`](https://github.com/choroscope/choroscope-spec) (available now) defines the configuration language for the platform. Every data "theme" in Choroscope needs to provide a configuration file to describe the data and how it should be visualized.
- `choroscope-db` (coming soon) is a Python-based utility that automates the creation of a geospatial ([PostGIS](http://postgis.net/)) database representing a data "theme." Though this database is intended primarily to serve as the data source for the frontend application, it may also be queried directly using PostGIS SQL, providing a powerful and open-ended way of exploring a geospatial data set.
- `choroscope-api` is a NodeJS server that makes the data contained in a Choroscope database (as created by `choroscope-db`) available as a web API. Though mainly intended to serve the needs of the frontend application, the API could also be used by other custom applications.
- `choroscope-app` is a frontend web application that visualizes the data provided by `choroscope-api`. Written in [TypeScript](http://www.typescriptlang.org/), the application leverages the mapping framework [Leaflet](https://leafletjs.com/) as well as a variety of other open-source technologies. It also provides a custom [WebGL-based renderer](https://github.com/ihmeuw/leaflet.tilelayer.glcolorscale) for visualizing pixel data.

For the Local Burden of Disease project, we've created additional resources for deploying the Choroscope application and its databases as containerized microservices. Our intent is that the platform itself be agnostic as to how and where it's deployed. To simplify the setup process for people who want to create their own instances of Choroscope, though, we also plan to publish generalized deployment resources, probably in the form of a [Helm Chart](https://helm.sh/) for deployment in [Kubernetes](https://kubernetes.io/).

## Where can I see Choroscope in action?

You can see a working instance of Choroscope in IHME's [Local Burden of Disease application](https://vizhub.healthdata.org/lbd). This application uses Choroscope to visualize estimates of population health. The Choroscope platform, though, is by no means limited to showing this kind of data. It can be used to visualize any data set, with any dimensions, using the same format. The IHME branding and navigation you see in the LBD application are in a layer separate from the core platform; they won't be included in the open-source offering.
