[![DOI](https://img.shields.io/badge/DOI-10.11582/2025.00041-blue)](https://doi.org/10.11582/2025.00041)

# MASSIMAL: A multimodal dataset for coastal habitat mapping in Norway

## Summary
The MASSIMAL dataset contains data from shallow coastal areas collected using multiple
data modalities, such as hyperspectral and multispectral aerial imaging, underwater
imaging, and sonar measurements. The dataset was collected at four main locations along
the Norwegian coast, in the time period 2021-2023, spanning large variations in habitat
types. The data is organized as a set of ZIP files, with each file corresponding to one
single time, location, and data type. Annotations of hyperspectral images are also
included in the dataset. Potential applications of the dataset include development of
mapping methods for coastal habitats based, education on coastal monitoring methods, and
reference material for timeline studies.

This introductory readme file is both part of the published dataset and part of the
[massimal-dataset](https://github.com/mh-skjelvareid/massimal-dataset) GitHub
repository. Any updates to the file will be posted to the repository. 

## The MASSIMAL Research project 
The MASSIMAL dataset was collected as part of the MASSIMAL project (Mapping of Algae and
Seagrass using Spectral Imaging and Machine Learning). The main goal of the project was
development of methods for shallow-water coastal habitat mapping based on hyperspectral
imaging from unmanned aerial vehicles (UAVs). However, multiple types of aerial and
underwater data was collected in the work towards this goal. 

The project was conducted in the period 2020-2024, and data collection and field work
was performed in the period 2021-2023. The dataset was collected during field campaigns
in four areas along the Norwegian coast; close to Bodø (67.2N, 15.0E), Vega (65.7N,
11.7E), Smøla (63.4N, 7.8E), and Larvik (59.0N, 10.1E). These areas were chosen to
represent multiple habitats of interest (e.g. seagrass meadows, kelp forests, maerl
beds) and to span large variations in environmental parameters (e.g. wave exposure and
water temperature). Multiple smaller locations were covered within each main area. 

The project was financed by the Norwegian Research Council (8 MNOK, project num. 301317)
and by UiT the Arctic University of Norway (600 kNOK), and was a collaboration between
UiT the Arctic University of Norway, the Norwegian Institute for Water Research, and Nord
University. 

Additional information about the project can be found on the following websites:

- [UiT project page](https://en.uit.no/project/massimal)
- [Cristin research database project
  page](https://app.cristin.no/projects/show.jsf?id=2054355)
- [Norwegian Research Council project
  page](https://prosjektbanken.forskningsradet.no/project/FORISS/301317)
- [SeaBee data portal with MASSIMAL
  data](https://geonode.seabee.sigma2.no/catalogue/#/search?q=massimal&f=dataset)


## Dataset modalities
The following list describes the types of data that are included in the dataset. The
names used are the same that are used for data type in the ZIP file names.

- hsi: Hyperspectral images collected with UAV
- msi: Multispectral images collected with UAV
- rgb: Color images (red, green, blue) collected with UAV
- usv: Underwater images and single-beam sonar data collected using a unmanned surface vehicle (USV)
- boat: Underwater images and/or written observations collected from a boat
- snorkel: Underwater images collected while snorkeling in the water surface
- rov: Underwater images collected using an ROV (remotely operated vehicle)
- walk: Images from the intertidal zone collected while walking
- annotation: Annotations of hyperspectral images (class "masks" for semantic
segmentation) 

Every type of dataset has a readme file which describes the data collection methodology
and dataset format in more detail. The readme files are also available at
[massimal-dataset/docs](https://github.com/mh-skjelvareid/massimal-dataset/tree/main/docs).


## Dataset file format and naming
The dataset is organized as a set of ZIP archive files, where each ZIP file corresponds
to a single set of data collected at a specific time and location. The ZIP files follow
the following naming pattern:

    massimal_<area>_<location>_<datetime[optional tag]>_<data type>.zip

A concrete example:

    massimal_vega_sola_202208231608-coast3_hsi.zip

This dataset was collected in the Vega area, close to the small island of Søla, on the
date 2022-08-23, at time 16:08. The dataset also has the additional tag "coast3". The
dataset contains hyperspectral images (HSI).


## Potential uses for the dataset
The original purpose of the dataset was to develop methods for mapping coastal habitat
types using optical remote sensing. This development was started during the project, but
there are many possible uses of the data to explore. For example, the hyperspectral,
multispectral and/or RGB images could be used as training data in large-scale machine
learning models for coastal mapping. The high-resolution hyperspectral images can also
be used to simulate the images from sensors with lower spectral or spatial resolution,
e.g. satellite sensors.

The multi-modal nature of the dataset enables exploration of how different sensors can
complement each other. For example, images from UAVs and sonar data from USVs can
potentially be combined to better map habitats across a large range of depths. Having
hyperspectral and multispectral images of the same area enables detailed evaluation of
the advantages and disadvantages of the two methods for coastal mapping. Having a large
set of underwater images also enables additional annotation of data.

Educators may find the dataset interesting as a practical example of coastal mapping at
high resolution and at a relatively large scale. Visualizing and interpreting multiple
layers of geospatial data could be interesting exercises for students of remote sensing,
machine learning, geography, oceanography, and ecology.   

The dataset may also function as a part of time series, documenting changes to the marine
habitats in Norway over time. 


## Details on hyperspectral images 
Since hyperspectral data was the main focus of the MASSIMAL project, some additional
information about the methodology and data format is included here.

Hyperspectral imaging was performed using an "Airborne Remote Sensing System" with a
Pika-L hyperspectral camera, both manufactured by Resonon. The imaging system was
mounted on a multicopter UAV with a camera gimbal. The hyperspectral camera had 300
spectral channels spanning the 400-1000 nm wavelength range, and the ground sampling
distance was approximately 3.5 cm. A spectrometer with a cosine collector mounted on the
UAV measured spectral downwelling irradiance. The hyperspectral images have units of
spectral radiance, and the measurements of downwelling irradiance enable straightforward
calculation of spectral reflectance. The image metadata also includes map information
for georeferencing each image. 


## Details on annotations of hyperspectral images
A subset of the hyperspectral images have been annotated. The annotation datasets
contain all annotations for hyperspectral images collected on the same day and
location, which in some cases encompasses multiple hyperspectral datasets. For example,
"massimal_vega_sola_20220823_hsi_annotation.zip" contains annotations from all 7
hyperspectral datasets collected on August 23. 2022. 

Annotations are formatted as pixel "masks", defined in the same pixel coordinate system
as the hyperspectral images. The annotations are not georeferenced, but georeferencing
can be achieved by copying the geotransform from the corresponding hyperspectral image.

The annotations were made in the online annotation tool "Hasty", and were exported in
three different formats:
- Colored PNG images + JSON file defining the classes and their color coding
- JSON file in COCO format
- JSON file in "Hasty" format (similar to COCO, but includes some additional metadata.)

The annotation classes are organized in a hierarchy with general habitat types (e.g.
"algae", "substrate") at the top, and more specific habitats (e.g. "kelp" or "Laminaria
hyperborea") as subclasses of the general types. In the JSON files all classes are saved
in a "flat" structure, but the hierarchy is defined in the readme file included with the
dataset, and can be used to group annotations as needed. 
