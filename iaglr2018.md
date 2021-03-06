# Who messed up my lake? <!-- .slide: data-state="hide-head" -->

<!-- .slide: data-background="img/front.png" data-background-size="contain" -->

<!-- ## Terry Brown, USEPA

http://tbnorth.github.io/iaglr2018

Use *Firefox*

i=0; while read; do python webshot.py '^iaglr2018$' $(printf test%02d.bmp $i) 68 5 5 5; i=$[i+1]; echo $i; done

-->



# Goals

 - Look at movement of nutrients in near shore
 - Tie land use to observed nearshore conditions
 - Examine influence on algal blooms (large scale /
   long term)
 - Look at impacts of land use decisions



# Harmful Algal Blooms

 - Public health
 - Environmental impact
 - Economic impact
 - Recreational impact



# Agents

- exist at a specific point in space
- can have multiple static and varying attributes
- can interact with surrounding agents (and cells)
  based on distance etc.
- added and removed from the model over the model's
  run-time


## Agents as individuals

![fish](img/fish.png)


## Agent Based Models (ABMs) and complexity

- run ABM with thousands of agents...
- competition for food / shade
- big fish / little fish
  - how does time spent hiding impact time
    spent feeding?
- test different behaviors / foraging
  strategies

Complexity more easily represented in ABMs


## Agents for continuous phenomena

- historically agent based modeling focused on distinct
  entities (fish in streams, etc.)
- modern computational power allows large numbers of
  agents to approximate continuous phenomena
- often used to model plumes / spills



# Contrib 1 <!-- .slide: data-state="hide-head" -->
<!-- .slide: data-background="img/nearshore_contrib0.png" data-background-size="contain" -->


## Contrib 2 <!-- .slide: data-state="hide-head" -->
<!-- .slide: data-background="img/nearshore_contrib1.png" data-background-size="contain" -->


## Contrib 3 <!-- .slide: data-state="hide-head" -->
<!-- .slide: data-background="img/nearshore_contrib2.png" data-background-size="contain" -->



# Hydrodynamic data

 - Dong Ko, U.S. Naval Research Laboratory (NRL)
 - POM (Princeton Ocean Model), 1 x 1 km x 25 layers
 - Lake Michigan, 2003-2015
 - 3 hour time step
 - Approx. 1 Tb of data for all 13 years



# Model overview

 - release 1 agent from each of 36 rivers each day
   - (once every 8 iterations)
 - agents released Jan. 1 are 365 days old at end of run
 - 19,236,960 records for 13,140 agents, 1.3 Gb NetCDF
 - Vectorized Python (numpy), 90 minute run time


## In a database

 - 19M records of `time, origin, birth, x, y, z`
 - use a netCDF file, treated as a 19M line array
 - hard to work out which lines contain which records
   - add agents every day (every 8 iterations)
   - might start removing agents in future
 - loaded into SQLite DB, same size file, fast indexes



# Where do they go?

 - nutrients mix / dilute / disperse, following them for 365
   days makes no sense, 7-21 days might
 - eggs, larvae etc. don't dilute, can be followed for longer
 - why not heat maps - agents spread quite thin,
   makes little difference


## NW 365 <!-- .slide: data-state="hide-head" -->

<!-- .slide: data-background="img/nw_main.png" data-background-size="contain" -->


## E Main <!-- .slide: data-state="hide-head" -->

<!-- .slide: data-background="img/e_main.png" data-background-size="contain" -->


## S Main <!-- .slide: data-state="hide-head" -->

<!-- .slide: data-background="img/s_main.png" data-background-size="contain" -->


## S Grn <!-- .slide: data-state="hide-head" -->

<!-- .slide: data-background="img/s_grn_bay.png" data-background-size="contain" -->



# Where did it come from?

```
python nsagent_contrib.py --start 20150901 --end 20150907 \
  testconf.json /mnt/edata/edata/large/nsagents/lastrun.nc \
  --max-age 56 --WSEN -87.9012 41.6959 -87.4333 42.1807 \
  --lbrt 0 0 155 150
Reporting iterations 1944-1992
Reporting from 9,11
Reporting to 63,48
425952 records in interval
Selected 5994 records by bounds
Selected 3696 records by age
Selected 163 agents
```


## Chicago <!-- .slide: data-state="hide-head" -->
<!-- .slide: data-background="img/chicago56.png" data-background-size="contain" -->


## Chicago <!-- .slide: data-state="hide-head" -->

<!-- .slide: data-background="img/chicago14.png" data-background-size="contain" -->

<!--

save from plt.show() after tight layout

mogrify -trim -border 10x10 -bordercolor white Figure_1* 

-->


## Anim <!-- .slide: data-state="hide-head" -->
<div style="position:relative;height:0;padding-bottom:75.0%"><iframe src="https://www.youtube.com/embed/8LHHP5tMndU?rel=0&amp;controls=1&amp;showinfo=0&ecver=2" width="480" height="360" frameborder="0" style="position:absolute;width:100%;height:100%;left:0" allowfullscreen></iframe></div>



# Depth

![](img/depth.png)



# A model built on a model...

 - real world validation (next slide)
 - test explanatory power (future work)



# Drifters

- real life agents, for model validation and real world measurements

![](img/IMG_20161117_141914.jpg)


## Drifter <!-- .slide: data-state="hide-head" -->

<!-- .slide: data-background="img/20180524_114738-1.jpg" data-background-size="contain" -->


## Drifter <!-- .slide: data-state="hide-head" -->
![](img/IMG_20161117_141247.jpg)


## Drifter <!-- .slide: data-state="hide-head" -->

<!-- .slide: data-background="img/IMG_20180524_124736638.jpg" data-background-size="contain" -->


## Drifter <!-- .slide: data-state="hide-head" -->

<!-- .slide: data-background="img/tracker.png" data-background-size="contain" -->


## Drifter <!-- .slide: data-state="hide-head" -->
<div style="position:relative;height:0;padding-bottom:75.0%"><iframe src="https://www.youtube.com/embed/gl_CFlBpERE?rel=0&amp;controls=1&amp;showinfo=0&ecver=2&start=60" width="480" height="360" frameborder="0" style="position:absolute;width:100%;height:100%;left:0" allowfullscreen></iframe></div>



# “Future” work

 - Retrospective tow data analysis
 - Refine correlation from ~1/4 lake scale to more
   immediate tributaries

![](img/towdata.png)



# Future work

 - Characterize nearshore composition for areas of interest
 - See if "problem" areas correlate to land use by water
   origin, as defined by agents
   - time scale for highest correlation?



# Questions?

![](img/wave.png)

Brown.TerryN@epa.gov

https://tbnorth.github.io/iaglr2018/



## Animation (a bit slower) <!-- .slide: data-state="hide-head" -->

<div style="position:relative;height:0;padding-bottom:75.0%"><iframe src="https://www.youtube.com/embed/04jy3JbZgic?rel=0&amp;controls=1&amp;showinfo=0&ecver=2" width="480" height="360" frameborder="0" style="position:absolute;width:100%;height:100%;left:0" allowfullscreen></iframe></div>

