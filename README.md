# Similar Artist Map <img src="https://raw.githubusercontent.com/NBPub/SimilarArtistMap/main/assets/favicon.ico" title="Similar Artist Map">

Visualize similar artist maps for musical artists in your library.

 - **Contents**
   - [Demonstration Site](#demonstration-site)
     - *[OnRender Website](https://similarartistmap.onrender.com/)*
	 - *[OnRender Source Code](https://github.com/NBPub/SimilarArtistMap_deploy)*
   - [Features](#features)
   - [Background](#background)
     - [Data Collection](#data-collection)
	 - [Network Mapping](#network-mapping-using-networkx)
   - [Local Installation](#local-installation)
     - [Requirements](#requirements)
 
 ## [Demonstration Site](https://similarartistmap.onrender.com/)
 
  - hosted on [render](https://render.com/), deployed by [Gunicorn](https://docs.gunicorn.org/en/stable/index.html)
    - `--workers=2`
	- speed may be limited by free tier hosting, can workers/threads be optimized for performance?
  - source code for site is located here, differences for deployment:
    - define `server` in [Dash app](https://dash.plotly.com/deployment)
	- set `Debug=False`
	
<details><summary>Screenshot - Widescreen</summary>

![wide](/screenshot_W.png "Similar Artist Map - Landscape") 

</details>

<details><summary>Screenshot - Tallscreen</summary>

![tall](/screenshot_V.png "Similar Artist Map - Portrait") 

</details>

<details><summary>Screenshot - Tallscreen, no neighbors</summary>

![no neighbors](/screenshot_V_nn.png "Similar Artist Map - No Neihgbors") 

</details>
 
 ## Features
 
  - Choose an Artist, then view it and its Similar Artists on an interactive network map. See images above.
    - Artists are colored to indicate whether they are in or out of the library. Learn how artists you know are connected, and find other artists to explore.
    - If a Similar Artist also has associated data, it will be added to the map, with the option to add even more similar artists: **add neighbors**
  - Information for each connection is provided by hovering over its midpoint.
  - Five network layout options are available, and a sixth, **Random**, produces a new result each time.
  
 ## Background
 
 This section describes how data was prepared and visualized for **Similar Artist Map**. 
 A detailed example is provided in two [notebooks](/background_notebooks/).
 
 *Note that packages were used in the notebooks that are not listed in [requirements.txt](/requirements.txt), as they are not needed for the site's deployment*
 
 ----
 
 ### Data Collection
 
 The data collection process is exemplified in detail in the [example notebook](/background_notebooks/Similar_Artist_Data_Collection.ipynb). 
 A brief overview is listed below, as well as some challenges.
 
  1. Gather list of musical artists from a library
  2. Query last.fm API to find up to 10 similar artists for each artist in library
  3. Save matches as JSON file
  
Some challenges were worked around rudimentarily, and could be improved by using last.fm API's [search](https://www.last.fm/api/show/artist.search) feature to properly match artists.

 - if an artist was not found and contained `+` or `&`, the symbols were replaced by `and` and the search was tried again
   - a list of alias names were saved to make data selection for graphing easier
   - alias names were not extensively used to determine if a found **similar artist** was in or out of the library
 - without using [last.fm Search](https://www.last.fm/api/show/artist.search), I could not fix queries for obvious artists, and they were not found, ex: `Jay-Z` 
 - some similar artists with a perfect match score, `1`, were simply 
   - alternate names / alternate representations of names `Jay Dee` <> `J Dilla`
   - closely related side-projects `MF Doom`

----
 
 ### Network Mapping using NetworkX
 
Network Graphs of Artists, Similar Artists, and their match scores were created using [NetworkX](https://networkx.org/documentation/stable/index.html).
Each artist was treated as a **node** and was connected to each of its similar artists by **edges** with **weights** related to match scores. 
When the networks were drawn, artist nodes were colored:
  - special color for artist of interest
  - another color for artists in library
  - another color for artists not in library

Various network options are discussed and displayed in the [example notebook](/background_notebooks/Similar_Artist_Network_Graphs.ipynb), 
as well as code for plotting in [matplotlib](https://matplotlib.org/stable/index.html) and [Plotly](https://plotly.com/python/).
The interactive Plotly figures were easily integrated into the demonstration site, which is a [Dash](https://dash.plotly.com/) application.

 
 ## Local Installation
 
   1. Create and activate a [virtual environment](https://docs.python.org/3/library/venv.html) in a directory
   
   ```bash
   cd path/to/your/directory
   python -m venv venv
   . venv/bin/activate # UNIX
   venv\Scripts\activate # Windows
   ```
   
   2. Copy [source code](https://github.com/NBPub/SimilarArtistMap/archive/refs/heads/main.zip) into your directory 
	 
   3. Install requirements via [requirements.txt](/requirements.txt) or install packages listed below without version specification
   
   ```bash
   pip install -r requirements.txt
   ```
   
   4. Use sample [artist data](/artist_data/) or generate your own data. Refer to [Jupyter Notebooks](/background_notebooks/) for guidance. Artist data should be saved in the `/artist_data/` directory.
   
   5. Run Dash application
   
   ```bash
   python -m app
   ```
   
   *Optional: Delete unneeded files and folders from your directory*
   
 
 ### Requirements
 
 *dependencies of the listed packages are not provided, see [requirements.txt](/requirements.txt) for full list of packages installed*
 
  - **[Python](https://docs.python.org/3/library/index.html) - 3.10 or greater recommended *(and likely required)* **
  - [Dash](https://dash.plotly.com/)
    - [dash-daq](https://dash.plotly.com/dash-daq)
	- [dash-bootstrap-components](https://dash-bootstrap-components.opensource.faculty.ai/docs/)
  - [NetworkX](https://networkx.org/documentation/stable/index.html)
    - [NumPy](https://numpy.org/doc/stable/index.html)
    - [SciPy](https://docs.scipy.org/doc/scipy/)