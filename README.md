# CalculatingT90forGRB
These codes provide three different methods for calculating T90 of Gamma Ray bursts
- **Unmask weighted** lightcurves
- **Mask weighted** lightcurves
- **Mask weighted with Bayesian blocks**
- 
- We need to create environment first. Below are the links for instructions:
- https://github.com/parsotat/BatAnalysis (Don't worry about Swift BAT Pattern Noise Maps)
- https://github.com/Swift-BAT/NITRATES.git
- 
- ***Instructions***
- 
- For unmask weighted
- To run the function, you first need to queue the data, then download it
- Then you should use ba.Batevent()function to create an event(Remember to add the coordinate)
- Then you should use event_name.event_files to save a file, and the location of that will be shown after you run it, that path is the event_file_path
- acs_file_path is in the directory "/PathtoyourDownloads/swiftID/auxil/", it has a suffix pat.fits.gz
- enb_mask_path is in the directory "/PathtoyourDownloads/swiftID/bat/hk/" it has a suffix bdecb.hk.gz
- output_dir is the directory where you want your output in
- Remember event_file_path is a file not a path, but other three path should include Path("path")
- Then you could run the function with the trigger time
- 
- For mask weighted
- To run the function, you first need to queue the data, then download it
- Then you should use ba.Batevent()function to create an event(Remember to add the coordinate)
- Then you could run the function with the trigger time
- 
- For mask weighted with Battblocks
- To run the function, you first need to queue the data, then download it
- Then you should use ba.Batevent()function to create an event
- Use .create_lightcurve() with a defined timedelta (e.g. 100 ms) to generate the light curve
- Then apply lc.set_timebins(timeinalg="bayesian")
- Then the data of t90 will be stored in lc.tdurs
- total_duration = (lc.tdurs['T90']['TSTOP'] - lc.tdurs['T90']['TSTART']).to('s').value
  print("Total duration:", total_duration)
  This command will give you the t90
