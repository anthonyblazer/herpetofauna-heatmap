# notebooks
This file contains the exploration notebooks and spike write-ups for this project. These are the observations and decisions that I will be making regarding the data and LLM training for this project.

### November 11th, 2026 - Determining training region
Results of querying iNaturalist on different region localities
*within 10 mi of Heflin: 22
within 25 mi of Heflin: 131
within 50 mi of Heflin: 614
within 100 mi of Heflin: 6,487
Alabama: 6,205*

Given that LLM training requiresa large dataset to properly train on, I will not train on a 10-mile or 25-mile region of the set location (though the 25-mile count can be useful for local testing). I will train on the 100-mile radius of Heflin because this allows for ecological accurate predictions since Heflin’s Piedmont setting is more similar to nearby Georgia than to south Alabama - a similarity that may get lost in analyzing Alabama state.
**Tradeoff**: some distant habitats may differ from Heflin, so I’ll hold out the ~131 observations within 25 mi as a local validation set. 
**Known bias**: observations cluster near Atlanta and other urban areas, to be handled with target-group background sampling.

### November 12th, 2026 - Evaluating background sampling data for Eastearn Box Turtle
 I decided to use target-group background sampling. A bias test using density of other-herp observations within 25 km gave AUC 0.749 for random background (strong observer bias) versus 0.444 for target-group background (bias largely removed, slight over-correction). 
 **Finding:** all 6,488 research-grade box turtle observations within 100 mi of Heflin are obscured by iNaturalist, so the habitat layer can only resolve roughly 10-25 km. **Caveats:** the target-group sample was the earliest ~6,000 records from 2023 on, not representative of the full period; the test uses one bias proxy, not a full model; presence points are blurred. 
**Follow-ups:** larger target-group pull, spatial-CV comparison of both backgrounds, assess precise-location data sources.

