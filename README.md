# CalculatingT90forGRB
This project provides three different methods for calculating the T90 duration of GRBs using Swift BAT data. All methods use Bayesian Blocks for adaptive time binning, but they differ in how the event data is weighted.
### 1. **Unmask Weighted**

- **Lightcurve Type**: Raw (unmask-weighted) lightcurve from Swift BAT event data. No mask weighting applied.
- **Use Case**: Better for analysis faint GRB.

### 2. **Mask Weighted**

- **Lightcurve Type**: Corrected (mask-weighted) lightcurve.
- **Use Case**: Better for GRB with strong signal. Easier to use.

### 3. **Mask Weighted with Battblocks**

- **Lightcurve Type**: Mask-weighted + binning via Battblocks.
- **Use Case**: Most precise method. Recommended for formal T90 measurements or bursts with complex time profiles.

## Environment Setup

Before running any method, make sure your environment is set up properly. Please refer to the following repositories:

- [BatAnalysis](https://github.com/parsotat/BatAnalysis)  
  *(Ignore Swift BAT Pattern Noise Maps)*  
- [NITRATES](https://github.com/Swift-BAT/NITRATES.git)

---

## Instructions

### Unmask Weighted

To compute T90 using **unmask weighted** data:

1. Queue the data and download it.  
2. Use `ba.BatEvent()` to create an event. *(Be sure to include coordinates)*  
3. Use `event_name.event_files` to generate and save a `.pickle` file.  
   - The output location of this file is your `event_file_path`.  
4. Define paths:  
   - `acs_file_path`: `/PathtoyourDownloads/swiftID/auxil/`, suffix: `pat.fits.gz`  
   - `enb_mask_path`: `/PathtoyourDownloads/swiftID/bat/hk/`, suffix: `bdecb.hk.gz`  
   - `output_dir`: desired directory for results  
   - *Note: wrap these paths with `Path("...")` where applicable*  
5. Run the T90 calculation function with your trigger time and these paths.

---

### Mask Weighted

To compute T90 using **mask weighted** data:

1. Queue the data and download it.  
2. Use `ba.BatEvent()` to create an event. *(Include coordinates)*  
3. Run the T90 calculation function directly with your trigger time.

---

### Mask Weighted with BattBlocks

To compute T90 using **BattBlocks**:

1. Queue the data and download it.  
2. Use `ba.BatEvent()` to create an event.  
3. Generate a lightcurve with time resolution (e.g., 100 ms):  
   ```python
   lc = event.create_lightcurve(timedelta=np.timedelta64(16, "100ms"), recalc=True)
4. Apply Bayesian binning:
   ```python
   lc.set_timebins(timeinalg="bayesian", save_durations=True)
5. Calculate T90:
   ```python
   total_duration = (lc.tdurs['T90']['TSTOP'] - lc.tdurs['T90']['TSTART']).to('s').value
   print("Total duration:", total_duration)


