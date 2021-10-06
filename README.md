# [EECS Project](https://eecs.oregonstate.edu/capstone/submission/pages/viewSingleProject.php?id=OMNUwhMqUjpqahZh): Learning the governing equations of ecological dynamics
Apply scientific machine learning methods to time-series from a three-year ecological field experiment to help disentangle the role of predator-prey interactions in driving the abundance dynamics of a species-rich community in the Oregon marine intertidal.

## Objectives
Scientific machine learning methods — which include the use of neural networks, symbolic regression, neural ordinary differential equations, and universal differential equations --- are a rapidly-developing means to learn the governing equations of both simple and complex system dynamics from data. Using these methods, the goal of the project will be to infer the equations (the model) that describes and predicts how predator-prey interactions influence population dynamics in the Oregon marine intertidal. The data for doing so comes from a unique field experiment in which species abundances and the feeding rates of a focal intertidal predator, the whelk _Nucella ostrina_, was monitored on a monthly basis for a total of three years. Progress towards achieving the goals of this project will serve as novel comparison to traditional (non-machine learning) methods of inferring and characterizing species interactions, and will lead to a better, predictive understanding of how complex ecological systems respond to the extrinsic and intrinsic perburbations.

## Motivations
Understanding how and why species abundances vary in space and over time represents a fundamental and pressing challenge for the field of Ecology. Many processes influence species abundances, including both extrinsic disturbances such as weather events, seasonality, and climate change, and intrinsic processes such as birth-death events, predator-prey interactions, and competition for limited resources. These multi-dimensional processes inherent to species-rich ecological communities mirror the processes that underlie complex adaptive systems in general.

## Data Overview
#### 9 Quadrats in 18 Patches
The experiment was conducted at Yachats Beach, OR.  In July 2013, we established 18 randomly-located _patches_ in the mussel bed of this site by scraping away all living material within them.  Each patch was created as a square, 1.5 x 1.5 meters in size, had large bolts drilled into two opposing corners so that it could be relocated over time.  The 18 patches are labelled by letters: _A, B, C,...,F, G, AB, AC,..., AE_ (there is no _AA_ patch).  Within each patch we established 9 randomly-located _quadrats_, each 25 x 35 cm large, by placing small bolts in two opposing corners.  The quadrats are numbered _1-9_ (hence _AC9_ refers to the _9th_ quadrat in patch _AC_).

The patches differ from each other in various ways, both for deterministic and stochastic reasons.  For example, they differ in their aspect and immediate surroundings, which affect how forcefully waves crash onto them. They also differ in their tidal height and hence how long they are submerged for each high tide. In this regard, all that we have data on is their tidal heights, hence in most regards we must assume the patches to be random samples of the intertidal from the population of potential intertidal locations that we could have sampled.

#### Abundance & Feeding Surveys
For the next ~3 years, we returned to the site each month to survey species' ensuing population dynamics.  That is, we followed the system's patterns of succession.  (A handful of months were missed due to dangerous wave conditions.)

Each month, two types of surveys were performed:

##### (1) _Abundance surveys_
Each of the 18 x 9 = 162 quadrats was photographed.  We then used [ImageJ](https://imagej.nih.gov/ij/index.html) to locate (x-y coordinates) and count the individuals of every identifiable "species" in (a subset of) the pictures.  Unfortunately, because of the amount of time required to process each picture, _only 3 of the 9 quadrats_ in each patch were processed over the entire duration of the time-series.  (Other EECS teams are working on automating the process.)  Therefore, the in-hand data consist of counts in each of 18 x 3 = 54 quadrats per survey.  (In each patch, the 3 focal quadrats are always the same 3 quadrats for the entire time series.)

**Focal species** -- There are [27 type categories](/data/data_orig/ExpPatch_SpeciesTypesID.txt) of "species".  However, the primary (prey) species of interest are the acorn barnacle [_Balanus glandula_](https://inverts.wallawalla.edu/Arthropoda/Crustacea/Maxillopoda/Cirripedia/Balanus_glandula.html) (_Bg_, Type 1), the gooseneck barnacle [_Pollicipes polymerus_](https://www.centralcoastbiodiversity.org/goose-neck-barnacle-bull-pollicipes-polymerus.html) (_Pp_, Type 11), and the mussel [_Mytilus trossulus_](https://www.centralcoastbiodiversity.org/pacific-blue-mussel-bull-mytilus-trossulus.html) (_Mt_, the combination of Type 7 and Type 15).  These are the most abundant species in the patches.  They are also the primary prey to the focal predator species, two _Nucella whelks_, whose feeding we have data on.

##### (2) _Feeding surveys_
Each month, we also performed feeding surveys of two predatory snails (whelks), [_Nucella ostrina_](https://www.centralcoastbiodiversity.org/northern-striped-dogwinkle-bull-nucella-ostrina.html) and [_Nucella canaliculata_](https://inverts.wallawalla.edu/Mollusca/Gastropoda/Prosobranchia/Order_Neogastropoda/Suborder_Rachiglossa/Family_Nucellidae/Nucella_canaliculata.html), in the patches.  Each survey was performed at the patch scale (not quadrat-specific) and consisted of a careful examination of every found individual to see whether it was feeding or not feeding.  (We typically tried to survey the whole patch, but often -- due to time or waves -- could only survey a fraction of the patch and the whelks within that fraction).

On the basis of the size of the whelk, the identity and size of its prey item, and temperature, we can back-calculate the "detection time" of each observed feeding event (i.e. the length of time that the whelk would, on average, take to feed on a prey item, which determines how likely we are to detect a feeding event).  Using these detection times ($d_i$) and the proportion of whelks that were caught in the act of feeding ($n_i / n$), we can calculate the whelk's feeding rate on each prey species ($f_i = \frac{n_i}{n}\frac{1}{d_i}$) in each patch (see [Novak et al. 2017](https://novaklabosu.github.io/publication/novak-2017-mo/) for details).

**Focal species** -- _Nucella ostrina_ is far more abundant that _Nucella canaliculata_, thus it's the former species' feeding behaviour that is of primary interest.

#### Temperature
Temperature is an important biological variable, dicating process rates at individual physiological scales (e.g., metabolic rates) to community and ecosystem scales (e.g., predator feeding rates).  We measured temperature using several TidBit data-loggers positioned at various locations around the site (both just below the lowest patch and just above the highest patch).  Measurements were taken every 15 minutes, thus encompass both low-tide (exposed => air) and high-tide (submerged => water) temperatures.

## Overarching Goal(s)
The overarching questions are, (how) can we (best) describe and explain
 (1) **the population growth rates of the species** (_as a function of their own abundance, the abundance of the other species, temperature, time (season), and/or space_)?,
 and/or
 (2) **the feeding rates of _Nucella ostrina_**  (_as a function of their prey species' abundances, their own abundance, temperature, time (season), and/or space_)?

While many "traditional" statistical methods have been tried, they all rely on knowing/assuming the "right" predator-prey population-dynamics model (or set of hypothesized models) _a priori_ and fitting it to the data to estimate parameters. [Recent work](https://royalsocietypublishing.org/doi/10.1098/rspb.2018.0422), however, offers the tantalizing prospect of learning the "right" model from the data itself.


## Machine Learning Resources
- [PySR: parallel symbolic regression built on Julia, and interfaced by Python](https://github.com/MilesCranmer/PySR)
- [YouTube: Automated Discovery of Mechanistic Models via Universal Differential Equations](https://www.youtube.com/watch?v=AKwqJxhKkoA)
- [YouTube: Discovering Symbolic Models from Deep Learning with Inductive Biases (Paper Explained)](https://www.youtube.com/watch?v=LMb5tvW-UoQ)
- [DiffEqFlux.jl – A Julia Library for Neural Differential Equations](https://julialang.org/blog/2019/01/fluxdiffeq/)

## Biology Resources


## Contact Information
[Mark Novak](https://novaklabosu.github.io) (mark.novak@oregonstate.edu)
