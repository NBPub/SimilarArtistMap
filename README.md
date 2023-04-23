# Similar Artist Map <img src="https://raw.githubusercontent.com/NBPub/SimilarArtistMap/main/assets/favicon.ico" title="Similar Artist Map">

Visualize similar artist maps for musical artists in your library.


 
 ## Demonstration Site [Link]()
 
  - to be hosted on some free service
  - list deployment specs
 
 ## Features
 
  - brief listing
  
 ## Background
 
 ### Data Collection
 
  - brief description and link to notebook
 
 ### Network Mapping using NetworkX
 
   - brief description and link to notebook
 
 #### matplotlib
 
   - brief description and link to notebook
 
 #### Plotly
 
   - brief description and link to notebook
 
 ## Requirements
 
 *dependencies of the listed packages are note provided, see [requirements.txt](/requirements.txt) for full list of packages installed*
 
  - **[Python](https://docs.python.org/3/library/index.html) - 3.10 or greater recommended**
  - [Dash](https://dash.plotly.com/)
    - [dash-daq](https://dash.plotly.com/dash-daq)
	- [dash-bootstrap-components](https://dash-bootstrap-components.opensource.faculty.ai/docs/)
  - [NetworkX](https://networkx.org/documentation/stable/index.html)
    - [NumPy](https://numpy.org/doc/stable/index.html)
    - [SciPy](https://docs.scipy.org/doc/scipy/)

 
 ### Local Installation
 
   1. Create and activate a [virtual environment](https://docs.python.org/3/library/venv.html) in a directory
   
   ```bash
   cd path/to/your/directory
   python -m venv venv
   . venv/bin/activate # UNIX
   venv\Scripts\activate # Windows
   ```
   
   2. Copy [source code](https://github.com/NBPub/SimilarArtistMap/archive/refs/heads/main.zip) into your directory 
	 
   3. Install requirements via [requirements.txt](/requirements.txt) or install packages listed above without version specification
   
   ```bash
   pip install -r requirements.txt
   ```
   
   4. Use sample [artist data](/artist_data/) or generate your own data. Refer to [Jupyter Notebooks](/background_notebooks/) for guidance. Artist data should be saved in the `/artist_data/` directory.
   
   5. Run Dash application
   
   ```bash
   python -m app
   ```
   
   *Optional: Delete unneeded files and folders from your directory*