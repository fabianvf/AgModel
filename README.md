# AgModel
 
## An _Agent-Based Model_ of the forager-farmer transition ##

[![DOI](https://zenodo.org/badge/12885/isaacullah/AgModel.svg)](http://dx.doi.org/10.5281/zenodo.17551)

AgModel is an agent-based model of a potential scenario for the forager-farmer transition. The model consists of a single software agent that, conceptually, can be thought of as a single hunter-gather community (i.e., a co-residential group that shares in subsistence activities and decision making). The agent has several characteristics, including a running population total, intrinsic birth and death rates, and an annual total energy need (measured in kcal), and an available amount of foraging labor. The model assumes a logistic, central-place foraging strategy in a fixed territory for a two-resource economy: millet and deer. The territory has a fixed number of millet patches, and a starting number of deer. While the model is not spatially explicit, it does assume some spatiality of resources by including search times.

Demographic and environmental components of the simulation occur and are updated at an annual temporal resolution, but foraging decisions are "event" based so that many such decisions will be made in each year. Thus, each new year, the foraging agent must undertake a series of optimal foraging decisions based on its current knowledge of the availability of millet and deer. Other resources are not accounted for in the model directly, but can be assumed for by adjusting the total number of required annual energy intake that the foraging agent uses to calculate its millet and deer foraging decisions. The agent proceeds to balance the net benefits of the chance of finding, processing, and consuming a deer, versus that of finding a millet patch, and processing and consuming that millet. These decisions continue until the annual kcal target is reached (balanced on the current human population). If the agent consumes all available resources in a given year, it may "starve". Starvation will affect birth and death rates, as will foraging success, and so the population will increase or decrease according to a probabilistic function (perturbed by some stochasticity) and the agent's foraging success or failure. The agent is also constrained by labor caps, set by the modeler at model initialization. If the agent expends its yearly budget of person-hours for hunting or foraging, then the agent can no longer do those activities that year, and it may starve.

Foragers choose to either expend their annual labor budget either harvesting deer or millet patches. If the agent chooses to harvest deer, they will expend energy searching for and processing deer. Deer search times are density dependent, and the number of deer per encounter and handling times can be altered in the model parameterization (e.g. to increase the payoff per encounter). Deer populations are also subject to intrinsic birth and death rates with the addition of additional deaths caused by human predation. A small amount of deer may "migrate" into the territory each year. This prevents deer populations from complete decimation, but also may be used to model increased distances of logistic mobility (or, perhaps, even residential mobility within a larger territory).

If the agent chooses to consume millet, then they extend time searching for a millet patch and processing the millet grains in that patch. Human selection preferences will drive evolutionary processes within the overall millet population, and the selection rate be altered as a parameterization of the simulation. Two characteristics are selected for: plant morphology (which affects both grain size and ease of harvesting), and patch density (reseeding density). These are generalized into two intrinsic populations of millet: “wild type,” and “domestic type.” Human harvesting will increase the overall ratio of domestic type millet plants in utilized patches over time due to artificial selection in patches that are under consistent use. The ratio will begin to decrease in patches that are not used according to a diffusion rate, and the proportion of wild to domesticated millet in all patches. Morphologically wild millet produces fewer kcal per seed, has longer handling times, and produces fewer seeds per patch. Thus, as millet is more frequently used, its desirable traits are enhanced (via selection), and it becomes more profitable. At the same time, however, there is a constant "diffusion" of wild-type characteristics back to patches so that if millet is consumed less frequently, the proportion of wild type millet will begin to increase in patches that are not used. Currently, millet patches are accessed in the same order every year, so humans are assumed to consistently choose the "best" patches first, if/when they decide to consume millet in a given year. The "size" of individual millet patches is set by the maximum wild/domesticated millet patch density values (default values assume patch size = 1 ha).

I have written AgModel in pure Python with the hope of better integration to scientific Python (e.g., pandas, matplotlib) and the open-science movement. The model has a simple graphical interface, or can be run “headless.” Optionally, experiments using parameter sweeps with repetition can be set up to run in parallel on as many available processors as desired. Careful parameterization of AgModel can test scenarios where complex hunter-gatherers engaged in foraging decisions that interacted with plant evolutionary dynamics to artificially increase the prevalence of domestic type plans in the local ecosystem. When the domestic phenotype is most prevalent, we can consider the species to be “domesticated.” The temporal dynamics of the process of domestication, however, are not linear, and the timeline and longevity of the domestication event may differ under changing environmental conditions. 


### References ###

The model is derived/inspired by ideas and data from the following scholarly works:

1. Bettinger, R.L., Barton, L., Morgan, C.T., 2010. The origins of food production in North China: a different kind of agricultural revolution, Evolutionary Anthropology 19, 9-21.

2. Winterhalder, B., Baillargeon, W., Cappelletto, F., Daniel, J., Prescott, I.R., 1988. The population ecology of hunter-gatherers and their prey, Journal of Anthropological Archaeology 7, 289-328.

3. Belovsky, G.E., 1988. An optimal foraging-based model of hunter-gatherer population dynamics, Journal of Anthropological Archaeology 7, 329-372.

## Installation and Running ##
You will first need to install Python 3 to run it. Depending on your operating system, you may need to use something like Anaconda to do this. On Linux you can use your package manager.

You will then need to install the following Python modules: 

* NumPy
* Pandas
* MatPlotLib
* EasyGUI

If you use the [PIP Python installer](github.com/pypa/pip), which is my preferred method of installation, you can try the following from the terminal:

`pip3 install -U numpy pandas matplotlib easygui`

 Once these are all installed, you just place the script in a folder of your choosing, open a terminal window in that same directory (you can often do this from the "right click" pop-up menu), and type `python3 AgModel-0.3.py`. The first window that will pop up will ask for a configuration file. I include a sample config file in this github repo that will parametrize the model for some interesting dynamics. There are default values that will populate the fields if  you choose to create a new config file. Then, there will be a window showing you the variables, and allowing you to change them. Anything you change will be saved to the config file you chose (so you can load them up again that way later). Once you've adjusted the parameters, the plotting canvas window will pop up, and it will ask you to if and how you want to start the simulation. If  you are just figuring out how to use the model, you may want to let some of the "realtime" text or plot updates occur so that you will be able to see what's going on in the simulation. These can slow the execution time by quite a lot, however, so you may wish to eventually run it without any realtime output. Once it's finished, you get the option of saving some output stats files as well as the plot. You can save any, all, or none of these: make sure to select all of the ones you want.

### Notes ###

* This software is released under the [GPL license](http://www.gnu.org/copyleft/gpl.html).
* Current release number is v0.4, which is a fully functional beta.
* Please cite as: __"Isaac I. Ullah, 2022. AgModel, version 0.4. http://dx.doi.org/10.5281/zenodo.17551"__ if you publish anything related to this software.

### Changelog: ###
v0.3 to v0.4
* upgraded to Python 3
* changes to GUI and interaction
* selection is now balanced against diffusion in utilized patches.
* diffusion is now density dependent, so that it reduces as the percentage of domestic phenotype in the ecosystem increases.
* added docstrings to classes and functions (no functional changes)

### Publications and Presentations ###

Barton, L., and Ullah, I. (2016) “Computer simulation and the origins of agriculture in East Asia,” Paper presented at the 7th Worldwide Conference of the Society for East Asian Archaeology, Boston, MA, June, 2016.

## Model Variables ##

<center>**Human Variables**</center>

Variable	| Default Value | Description
----------- | ------------- | ---------------------------------------------------------------------------------------------------------------------
people 		| 50.0   		| The initial number of people in the band
maxpeople 	| 500 			| The maximum human population (just to keep this in the realm of possibility, and to help set the y axis on the plot)
hbirth 		| 0.04   		| The annual human per capita birth rate
hdeath 		| 0.03  		| The annual human per capita death rate
starvthresh | 0.8 			| The starvation threshold (percentage of the total kcal below which people are starving, and effective reproduction goes to 0)
hkcal 		| 547500.0 		| The number of kcals per year required per person
fhours 		| 4380  		| The number of foraging hours available per person
hgratio     | 0.5           | The ratio of hunters to gatherers in the population (for allocation of time budgets)

<center>**Deer variables**</center>

Variable	| Default Value | Description
----------- | ------------- | ---------------------------------------------------------------------------------------------------------------------
deer 		| 4000.0  		| The initial number of deer in the hunting region
maxdeer 	| 6000.0  		| The maximum number of deer that the region can sustain (carrying capacity) without human predation
dmigrants 	| 10  			| The number of new deer that migrate into the territory each year (keeps deer pop from being totally wiped out)
dbirth 		| 0.065  		| The annual per capita birth rate for deer
ddeath 		| 0.02  		| The annual per capita natural death rate for deer
dret 		| 158000.0   	| The return rate (number of kcals) per deer killed
ddsrch 		| 72.0  		| The density dependent search costs for deer (hours time expended per recovery of one deer at the density "ddens")
ddens 		| 1000  		| Density of deer for which search cost "dsrch" is known
dpatch 		| 1.0  			| Number of individual deer encountered per discovery
dhndl 		| 16.0  		| The handling costs for deer (hours handling time expended per deer once encountered)

<center>**Millet Variables**</center>

Variable	| Default Value | Description
----------- | ------------- | ---------------------------------------------------------------------------------------------------------------------
millet 		| 500  			| The number of millet patches in the gathering region (assume a patch is ~1ha)
mretw 		| 0.0507  		| The return rate (number of kcals) per wild-type millet seed
mretd 		| 0.1014  		| The return rate (number of kcals) per domestic-type millet seed
mprop 		| 0.98  		| The starting proportion of wild-type to domestic-type millet (1.0 = all wild, 0.0 = all domestic)
mselect 	| 0.03  		| The coefficient of selection (e.g., the rate of change from wild-type to domestic type)
mdiffus 	| 0.02  		| The coefficient of diffusion for millet (the rate at which selected domestic traits disappear due to crossbreeding)
msrch 		| 1.0  			| The search costs for millet (hours expended to find one patch of millet)
mpatch 		| 880000.0 		| Number of millet plants per patch at the start of the simulation (individuals encountered per discovery)
maxpatch 	| 1760000.0 	| Maximum number of millet plants that can be grown per patch (a bit of a teleology, but we need a stopping point for now)
cultiv 		| 5000 			| Number of additional millet plants to added to a patch each year due to proto-cultivation of the patch. The patch reduces by the same number if not exploited.
mhndl 		| 0.0001  		| The handling costs for millet (hours handling time expended per seed once encountered)

<center>**Simulation Controls**</center>

Variable	| Default Value | Description
----------- | ------------- | ---------------------------------------------------------------------------------------------------------------------
years 		| 500  			| The number of years for which to run the simulation

### Notes on the default values used
1. Domestic millet produces 1014 kcal/kg, yielding 1000 kg/ha from seeds dispersed at 10 kg/ha, with 176,000 seeds per kilogram (so 1.76 million plants per ha), and a return rate of about 500 kcal/hr once encountered. Assume patch size is one hectare. Data on domestic millet comes from the UN-FAO: [http://www.fao.org/ag/AGP/AGPC/doc/gbase/data/pf000280.htm](http://www.fao.org/ag/AGP/AGPC/doc/gbase/data/pf000280.htm).
3. Wild millet: Currently, in lieu of hard data on wild millet, the default wild millet values are derived by assuming they are half as much as those of domestic millet. 
4. Deer produces 1580 kcal/kg, with 100 kg yield per animal, and a return rate of about 10000 kcal/hr once encountered. Two fawns per year are assumed and three days average search time when there are 1000 animals in the vicinity. Some of these are estimates from Bettinger 1991, "Hunter-Gatherers," and some come from [USDA nutrition info for vennison](http://ndb.nal.usda.gov/ndb/foods/show/5421?fg=&man=&lfacet=&count=&max=25&sort=&qlookup=game+meat&offset=25&format=Full&new=&measureby=).
5. Note that this model assumes storage of millet, but not of deer.
