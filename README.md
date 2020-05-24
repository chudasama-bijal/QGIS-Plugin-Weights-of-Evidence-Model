<img src="https://github.com/geoportti/Logos/blob/master/geoportti_logo_300px.png">

QGIS Plugin: Weights-of-Evidence (WofE) Model
=============================================

This plugin implenents the Weights-of-Evidence (WofE) model on geotiff raster files for mineral prospectivity modelling in QGIS.
The ‘weights-of-evidence’ (WofE) model is a Bayesian method to estimate the probability of a hypothesis (H) based on the knowledge of occurrence of certain evidential events (E). It involves quantification of spatial association (i.e. the weights) between the targeted event (the hypothesis) and the evidential event (the evidence). 

This plugin is created particularly for mineral prospectivity modeling, therefore the hypothesis to be predicted  is the occurrence of the targeted mineral deposit and the ‘evidential events’ are the datasets representing geological features such as lithology, structures, whole rock geochemistry etc. The occurrence of a mineral deposit can be associated with either the presence or the absence of an evidential event. In WofE model the spatial association (i.e. weights) between the deposit and (the presence/absence of) a particular evidential event is assessed by estimation/prediction of posterior (conditional) probabilities using Bayes’ Theorem.

Mathematically, the WofE model has two parts:
1. Quantifying the spatial association (i.e. weights) between the deposit and the evidential events.
1. Updating the posterior probabilities of the deposit occurrence by combining the weights-of-evidences of all the events.

Implementation of the WofE model to mapping the potential of a mineral deposit is accomplished through the following steps in this WofE plugin:
1. Calculation of weights-of-evidences for multiclass (multi-feature) evidential events,
1. Reclassification of multiclass (multi-feature) evidential events to binary evidential events, based on the weights-of-evidences,
1. Recalculation of generalized weights-of-evidences after reclassification, and
1. Calculating posterior probabilities by combining the generalized weights of all the evidential events.

Plugin installation files and instructions
====
This pluigin works in QGIS 3.6 and above (Python 3.7.0). Python libraries required for calculations in this plugin are:
+ GDAL
+ Numpy
+ Pandas

Plugin Installation 
----
The files included in the installation package are:
1. wofe_module.zip: Plugin installation file.
1. Pandas.zip: Pandas library, downloaded from: https://pandas.pydata.org/
1. Sample_data.zip: Test data for plugin implementation. (Data provided by the Geological Survey of Finalnd).
1. Results.zip: Results from the plugin (for sample datasets provided for plugin demonstration).

Download each file individually and refer to the [user manual](https://github.com/chudasama-bijal/QGIS-Plugin-Weights-of-Evidence-Model/blob/master/QGIS-WofE-Plugin%20User%20Manual.pdf) for detailed instructions on installation of this plugin in QGIS.

Plugin Tools
----
The WofE plugin has three tools: 
1. Pre-process Data
1. Calculate Weights
1. Calculate Responses

### Pre-process Data Tool

#### I. The 'Pre-process Data' Tool:
1. Creates the training data, 
1. Clips the evidence rasters to the extent of the mask layer, and 
1. Resamples the evidence rasters to the unit area of each training site.
 
#### II. Calculate Weights Tool 
The ‘Calculate Weights’ tool should be implemented individually for each evidence raster. It executes the following calculations: 
1. Estimation of prior odds of occurrence of a mineral deposit per unit cell of the study area, 
1. Reclassification of numerical multi-class evidence raster into the ‘Favorable’ and ‘Unfavorable’ binary evidence raster, and 
1. Estimation of the weights of evidence for individual reclassified binary evidence raster or categorical evidence raster using the Bayes’ Rule. 
 
#### III. Calculate Responses Tool 
This tool calculates the posterior probability for occurrence of a deposit by combining the prior odds and the 'weights-of-evidence rasters' calculated in the ‘Calculate Weights’ tool.

**The final results include:**
+ **Posterior Probability Raster:** The values in this raster are the prospectivity values for occurrence of a deposit. 
+ **Standard Deviation Raster:** This raster contains the standard deviations in the posterior probability calculations because of the standard deviation of weights of the evidence rasters. 
+ **Confidence Raster:** This raster represents the confidence of the prospectivity values obtained in the Posterior Probability Raster. 

The [user manual](https://github.com/chudasama-bijal/QGIS-Plugin-Weights-of-Evidence-Model/blob/master/QGIS-WofE-Plugin%20User%20Manual.pdf) provides detailed demonstration for implementation of the WofE plugin tools with the sample datasets (Source of data - Geological Survey of Finland) in QGIS.

Citing
=====
When using this plugin, please cite the oGIIR project: "We made use of geospatial data/instructions/computing resources provided by the Open Geospatial Information Infrastructure for Research (oGIIR, urn:nbn:fi:research-infras-2016072513) funded by the Academy of Finland."

Authored by Bijal Chudasama, Geological Survey of Finland. www.gtk.fi
