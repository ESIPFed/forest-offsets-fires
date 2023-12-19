# Real-time visualization of satellite-derived active fire data to support monitoring of forest offset projects

ESIP Lab Pilot Project for the Wildfire & Water RFP led by [CarbonPlan](https://carbonplan.org/).

## Short project description

There is a rich archive of near real-time, satellite-derived active fire data that informs wildfire management. However, accessing this data can be challenging, limiting use in research and planning. We propose lowering the barriers to using these data by developing open, reproducible data management workflows and tutorials. We will demonstrate how to use these new fire data by incorporating these real-time data into our existing forest carbon offset project fire monitoring tool. Augmenting this tool will support ongoing public monitoring and reporting about forest offset projects burning throughout the 2023 United States fire season.

## Project overview

For the past two years, CarbonPlan has operated a [fire and offset project monitoring tool](https://carbonplan.org/research/forest-offsets-fires) that tracks when wildfires burn within the boundaries of forest carbon offset projects in the United States. The tool has enabled researchers, journalists, and the public to monitor forest carbon offset outcomes, and has received [substantial media coverage](https://www.nytimes.com/2021/08/23/us/wildfires-carbon-offsets.html). The current tool displays the boundaries of forest carbon offset projects and the boundaries of all wildfires that have burned during the current calendar year, as provided by the National Interagency Fire Center (NIFC). In addition to displaying these geographic datasets, the tool provides summary statistics about burned acreage on both a per project basis and across all monitored projects.

However, there is often a delay in the creation of NIFC fire boundary shapefiles, hampering active fire monitoring efforts. The boundaries are developed via mixed methods and combine data from satellites, on-the-ground reports, and airborne measurements. Because active fires can change dramatically over the course of even a single day, NIFC boundaries do not always reflect the full extent of a fire. This monitoring problem is especially pronounced for small, early-stage fires with little or no management, with some fires not even existing in the catalog of NIFC shapefiles.

The NASA-sponsored Fire Information for Resource Management System (FIRMS) presents a near real-time alternative. Based upon a composite of Moderate Resolution Imaging Spectroradiometer (MODIS) and Visible Infrared Imaging Radiometer Suite (VIIRS), FIRMS provides ready access to thermal anomaly data (interpretable as “active fires”) for the entire globe at moderate spatial resolution (i.e., 375 meters) and at a daily time step.

While NASA visualizes the FIRMS data on their own [map](https://firms.modaps.eosdis.nasa.gov/map/#d:24hrs;@0.0,0.0,3z), the underlying dataset is challenging to access, limiting widespread research and applications outside of the FIRMS platform. The New York Times has developed a [map tracking wildfires](https://www.nytimes.com/interactive/2022/us/fire-tracker-maps.html) based upon the FIRMS data, but their data and workflows are not publicly available, nor do they showcase any information related to forest offset projects. We propose developing a new, cloud-optimized version of the FIRMS active fire dataset. By making this dataset more accessible we will promote use by a broader research and journalist community, and also enable updates to our forest offset project monitoring, as described below.

We will ingest the data into our existing fire and offset project monitoring tool, enhancing the types of visualizations we're able to produce and allowing us to provide additional context and commentary when reporting on actively burning projects. For example, rather than relying on static boundaries, we will be able to highlight active portions of a fire and convey information about how a fire has changed over time. The motivation to include these data in the platform is directly informed by the work we have done for the past two years. During the early stages of a fire, when NIFC data is most likely obsolete, we have relied on an independent, manual workflow to overlay FIRMS data with offset project boundaries. When we see a large change in the number of active fire pixels, we use that information in deciding when to publicly announce that an offset project is burning. This grant would provide funds to formalize those workflows, data storage/formatting, and revisions to the front-end tool to allow us to display active fire pixels and, at the same time, make the transformed fire data accessible to a broad audience.

## Final report

We created an open source pipeline to generate a cloud-optimized GeoParquet dataset for active and recent fires, along with vector tiles for performant visualization. The code for generating the dataset is released under an MIT-license in the [carbonplan/forest-offsets-web](https://github.com/carbonplan/forest-offsets-fires) GitHub repository. The pipeline uses a composite of thermal anomaly data from the Visible Infrared Imaging Radiometer Suite (VIIRS) aboard Suomi-NPP and NOAA-20 and the Moderate Resolution Imaging Spectroradiometer (MODIS) aboard Terra and Aqua from the NASA-sponsored [Fire Information for Resource Management System](https://firms.modaps.eosdis.nasa.gov/) (FIRMS). We filter out low confidence data and subset to only include thermal anomalies within the United States. We leverage the Protocolbuffer Binary Format for vector tiles for performant visualization on the web. The data pipeline is run every 6 hours using GitHub actions.

We added the active and recent fires dataset to CarbonPlan's [fire and forest offsets monitoring tool](https://carbonplan.org/research/forest-offsets-fires). We use the opacity of the data in the monitoring tool to highlight the fire radiative power. The vector tiles approach effectively highlights active fires when the user is zoomed out and provides context about the active fire front when zoomed in. We published all the code for the monitoring tool in the MIT-licensed [carbonplan/forest-offsets-web](https://github.com/carbonplan/forest-offsets-web) GitHub repository.

We published a [blog post](https://carbonplan.org/blog/forest-offsets-firms) on the addition of the satellite-derived, near real-time data to our monitoring tool. We have also engaged with journalists about offset projects burning (e.g., [reporting on the Bootleg Fire](https://www.opb.org/article/2023/08/02/climate-change-carbon-offset-oregon/)). Lastly, we developed a [tutorial](tutorial/fire-monitoring.ipynb) about our workflow. We will present the results at the January 2024 ESIP meeting.

## CarbonPlan

CarbonPlan is a nonprofit organization that uses data and science for climate action. We aim to improve the transparency and scientific integrity of climate solutions with open data and tools. Find out more at [carbonplan.org](https://carbonplan.org/) or get in touch by [sending us an email](mailto:hello@carbonplan.org).

## License

All the code in this repository is [MIT](https://choosealicense.com/licenses/mit/)-licensed, but we request that you please provide attribution if reusing any of our digital content (graphics, logo, articles, etc.).

