---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Change Log

<div align="left"><figure><img src="../.gitbook/assets/DX+_blue@300x.png" alt="" width="188"><figcaption></figcaption></figure></div>

## Versions

***
## 2025.51 (released 2025-12-17)

* New Features
  * Video Input added
    * Added support for video input in plots, allowing video from file, datastore, or live recorder, with time-synced display alongside sensor data.
  * Model and Simulation integration added
    * Adding ability to enable the use of simulation data and models within DX+ for analysis and visualization.
  * Pull setup button will highlight when changes were applied that require pull setup to be re-clicked
  * Added support for IRIG timing signals
  * Clicking submit design automatically takes user to the Viewing page
  * Plotting:
    * Scatter plot added
    * Tracking plot added
    * Bar plot added
    * Reset data button added to plot options for relative plots
    * Plot Linking added to plot tools ribbon
    * Y-axis offset option added for visual stacking
    * Markers/Cursor sticks added to Y-axis
    * Y-axis scale set to half auto as default for scatter plots
    * Auto title feature added to plot options, automatically on
  * New Designer Elements
    * Inputs
      * DewesoftNet
    * Processors
      * Stream Selection
      * Time Aligner
      * Signal Math
      * Static Fit
      * Mode Fit
    * Outputs
      * DATX File Writer
      * RWX File Writer
      * Model Transmit
      * Model Viewer
      * IDDS Transmitter
  * UI Changes:
    * All designer elements have updated icons
    * Designer page > all ribbons have updated icons
    * Viewing page > all ribbons have updated icons
    * Viewing page > added tabs for video and model
    * Installer page UI/UX improvements
* Fixed Bugs:
  * Apex Licesense Manager and Installer Fixes
    * 1613 failure with ALM on first startup/initial install.
    * 1616 failure with ALM on restart.
    * 1072 ALM crash when license server is down.
    * 1382 Switching to licesne server when there isnt one caused various issues.
    * 2085 Fixed various installer and Apex License Manager issues, including errors during installation, problems launching the license manager, and license application inconsistencies.
  * User Interface Fixes
    * 1431 Page status section in the ribbon could be clipped at smaller window sizes in the DX+ Viewer.
  * Plotting Fixes
    * 1075 Campbell indexing issue with displaying OrderFFT data.
    * 1377 Campbell plot hang with analog trigger tach.
    * 1846 Using absolute time wouldn't show date/time with point selection.
    * 1917 Plot settings dialog would not display when activated through context menu.
    * 2014 Plot sliders would not hide when time sync was enabled.
    * 2070 Plot options dialog would not open after resubmit.
    * 2105 Plot settings would not work when pop-out.
    * 2135 Fixed issue where reloading saved scatter plots placed all traces at the zero x-axis.
    * Starting and stopping DAQ, all Campbell plot peaks would appear at speed 0 until the plot is reloaded, randomly would occur.
    * 1957 Issue would occur when displaying time vs time data with FFT's Campbell plot.
    * 1167 Peaks would permanently disappear in Campbell and Zmod plots if the threshold was set too high.
    * 2157 When adding new plots after disabling time sync, crashes would occur.
    * 2125 Disabled channels in offline mode still appeared in the Viewer tree.
    * 2153 Newly added plots with time sync would still show individual sliders.
    * 2082 XY-plots had misaligned time between time based traces.
    * 2088 Plot export(print) would previously not show graphic plots.
    * 2091 Full/Half auto scaling, time offset, and markers would not work on stack traces.
    * 2095 Gauge Values for tach2 and tach3 would previously display unstable/rapid changing decimal values.
    * 2038 Time offset traces were previously not able to be selected in plots.
    * 1910 Tabulated plot windows would not close when quitting DX+.
    * 1693 Right clicking on a plot and selecting "tabulate" would cause a crash.
    * 1694 Cursers could previously not be moved; improved cursor selection, dragging, and context menu responsiveness for all cursor types.
    * 1696 Pointer tool is now selected by default.
    * 1696 Clearing markers now updates the plot immediately.
    * 1696 Graphic plot labels now have improved scaling and performance.
    * 1582 Text plots would appear in arbitrary order when dragged form viewer tree, now they maintain correct order.
    * 1650 XY plots would not save or restore selected data components for the x/y axes, causing incorrect plot outputs after reload.
    * 1432 Marker arrows in DX+ Viewer would not scale correctly when plots where maximized.
  * Performance Fixes
    * 1219 DX+ would be unresponsive when submitting a design as DAQ was running.
    * 1230 Pulling setup from device or DS overwrites previously enabled/disabled items.
    * 1085 Data Simulator unselected channels appeared in the viewer.
    * 1870 Selecting stale Viewer elements or channels from removed components caused crash.
    * 1875 Octave Band design issues in the design untill pull set up was completed.
    * 1918 Activating QAquire button through a released package would cause a crash.
    * 1953 Multiple inputs into the Rev Resample would cause streams to now be correctly selected nor propegated.
    * 2012 Limits would not save when using Data Simulator.
    * 2090 Errors with Sqlite input data would cause application freeze.
    * 2113 Improved thread handling to prevent crashed when canceling in post processing with sqlite read operations.
    * 1874 Added more error handling to ensure errors were getting reported to users.
    * 1754 Error messages would not appear after first popup has happened.
    * 1856 Designs with errors would not show errors until design was opened twice.
    * 2114 Processing would continue after a setup error, error is now shown to the user.
    * 2116 If a design was submitted and resulted in an error but was fixed then resubmitted, the design would continue to not work.
    * 2013 Deleting plots would sometimes cause a crash.
    * 2065 Re-submitting DS designs would occasionally cause a crash.
    * 2145 Processing multiple data points/records with Sqlite files was prevented, now supports batch processing as intended.
    * 2089 SQLite input would periodically buffer the longer it played.
    * 2096 Entering decimal numbers was previously difficult in EU Scalar and similar entry elements.
    * 1591 Page status no longer remains when DX+ is closed.
    * 1603 DX+ Viewer's ribbon button no longer changes locations when window size changes.
    * 1626 Ram usage previously would sometimes show incorrect values
    * 1628 Data Simulator would not load parametter or speed streams correctly, preventing the viewer from enabling.
    *



## 2025.15 (released 2025-04-15)

* Updated Installer
  * Added ability to select individual devices, processors, outputs, etc. for installation
* Separated and Named Apps Based on Functionality
  * DX+ Data Acquisition
  * DX+ Analysis
  * DX+ File Viewer
  * DX+ Remote Viewer
* Plotting Updates
  * Added Plot Selector Dialog
  * Added Signal vs. Signal capability for Time, History & Strip plots
* New Designer Elements
  * Input
    * Audio Input
    * Cyres
    * Scanivavle Device
    * Apex-H5 (offline mode)
    * CADDMAS-H5 (offline mode)
  * Output
    * Apex-H5 (HDF5)
* Updated Designer Elements
  * FFT & DFT elements have been combined
    * "Mode" option enables switching between FFT & DFT
  * Tach element settings now support digital and analog trigger options 
  * Added Help tab to element settings panels to easily reference documentation about elements & API
* Renamed Items
  * DX+ Subscriber Element -> Receive Element
  * DX+ Publisher Element -> Transmit Element
  * Peak Processor Element -> Adv. DSP Element
  * Apex DX+ Subscriber Connection (Viewer) -> DX+Net Receiver
  * Time Plot -> Scope Plot
* Fixed Bugs
  * Plot Functionality
    * Plot Auto Axis scaling not working
    * Ribbon Axis min/max doesn't correctly handle steady state values
    * Bar plot cannot perform remove trace / clear traces
    * Unable to pick points / place markers on Bar Plots
    * Legend Settings are not applied when Legend Type is set to Internal
    * Plot information text box defaults to white, making it invisible on white plots
    * Frequency Sweep Simulator Units not showing up
    * Legend Font Size does not work
    * Peaks output lags behind FFT
    * Inconsistent Strip Chart behavior
    * Trace Does Not Update with Axis on Playback Plots
    * Plot Options Blank
    * Auto and Half-Auto scaling having issues in some plots
    * Viewer Not Loading Non-Datapoint Data
    * Plot Setup Loading not working
    * Campbell gets overwhelmed with FFT
    * IIR Filters missing Filter Prototype Selection
    * Limits Traces added/removed incorrectly
    * Trace line colors missing from legend
    * Strip Chart Shows 1969 absolute time
    * WARN Level not applying for plot coloring (Always red)
    * Plot Reload in Viewer is Slow
    * Plot Settings Reset When New Design Submitted
    * Orbit Plot Flashing
    * FIR/IIR Filters auto-size determination not working
    * Graphic Plots Display issues
    * Time, History, and Strip Plots Show Same Trace
    * Pan Tool Sticks to Plots
    * Plots Cannot be Created from Peaks Output
    * Hist and Strip auto ranges not working
    * Strip Chart Slow
    * Bar Plots not scaling correctly
    * External Legend Issue
    * Octave Bank Processor not Getting Correct Input Sampling Rates
    * Cannot Create Multiple Speed Campbells
    * Bar Plots Not Functional in Offline Analysis
    * FFT Processor Sets Resolution instead of Block Size
    * Octave Plots X Axis Does Not Show All Values
    * Plot Options are too tall for 1080p screen
    * Plot Spaces cannot be Deselected if All Spaces are Selected
    * DX+ Peaks element produces no graphable data
    * Strip Chart Y-axis not auto scaling for P2A Signal
    * Saved viewer page with History plot doesn't load X axis range
    * Order FFT Campbell vs P(N) can freeze during load
    * Campbell Slow down issue over long duration
    * Freq Sweep Sim drops out occasionally
    * Zmod - Similar issues to Campbell (Plotting scatter)
    * Peak Processor Chan. # does not update with a new file in RWX - resets to 0
  * User Interface
    * Component Settings and Streams tabs can disappear or overlap
    * File menu not wide enough to show filenames
    * Ribbon Popout buttons missing icons
    * Viewer file menu says About DX+ incorrectly
    * Pause buttons on playing plots reset to play icon when style changes
    * Bar chart slider styled incorrectly
    * Bar plot buttons missing icons
    * DX+ Plot Pages window can obscure the Save Successful dialog
    * DX+ File>Open error message isn't descriptive
    * DX+ Receive can incorrectly stop/start DX+ Transmit 
    * Submitting Design with Existing Plots Enables Plot Playback Slider
    * DX Plus about dialog missing logo
    * Plot placement during multiplot creation places plots in different order than the tree
    * Plot Selection "Loses Focus" or becomes stuck
    * Elements can be placed on top of each other
    * Can't switch to Viewer/Designer in full screen mode
    * DX+ File menu doesn't close after clicking an action
    * All plots do not remain selected after '1 Trace Per' action
    * Designer Ribbon Resizes Incorrectly
    * Context Menu displaying incorrectly
    * 'Remove Connection' option not working on components
    * Usage Indicator not Showing in Ribbon
    * Units missing in various displays
  * Data Processing
    * Issue with Tach Processor when Tachometer Level set to 0
    * Tach Stream passed incorrectly from Rev Resample Element
    * DX+ SQLite Input error issues
    * Changing properties in elements doesn't mark design as changed
    * Copy & Paste SQLite Input doesn't populate with streams
    * Rev Resample Always Returns first Rev if PPR Less Than 1
    * IIR Filter has no filter types
    * Datatel Device not streaming slow data
    * DS device stats not working
    * Processor items connection issues
    * EU Scalar Element needs way to specify Units
    * Trigger Processing Settings Allow negative threshold
    * Octave Banks and Statistics Channel Issues when connecting
    * Avg Statistic Not Returning Expected Results
    * Tach processor not working as expected
  * File Management
    * Pressing "Cancel" on save design window still opens file selection
    * Open Design with DataSim Error
    * Successfully saved designs won't load elements, only outputs
    * Loading saved design not working
    * DX+ "Submit Design" not enabled after opening a design
    * DX+ File>New Design doesn't clear outputs
    * Loading plots from saved plot layout doesn't apply limits
    * Loading Designs does not load saved settings
    * Edited names do not come back when loading saved design
    * Saving Plot Layouts does not work
  * Other Issues
    * When an error occurs on start, the DAQ should call stop
    * DAQ is sometimes uninitialized after Submit Design and going to Viewer
    * Datastore records with -1 timestamps showing
    * X Axis should be static time windows for History and Time Plots
    * Updates need to occur per page
    * Plot Slowness When Switching Pages
    * Trace settings changed in ribbon don't apply until plot options are opened
  * Performance Issues
    * DAQ Control Not Hiding in Offline Analysis Mode
    * Apex Data Simulator stream badge updating incorrectly
    * License Manager token count incorrect with Statistics streams
    * Page numbering doesn't return to zero
    * Recording indicated with no DB filename defined
    * Changing Design and Submit while system is running
    * Outputs "Inputs" selections not reflected in "Streams" Tree
    * Tree does not contain processed results when loading a design
    * Num Connections on PSQL Output not keeping input value
    * When deleting elements from canvas, they still appear in component list
* Fixed Items for Improved Stability
  * Design Operations
    * Crash when creating plot pages from DS Receiver
    * Crash when clicking Submit while design is saving
    * Crash when clicking Transmit output element after submitting design
    * Crash after doing New Design and trying to Remove outputs
    * Crash when clearing unsaved design when changing from DAQ to Offline mode
    * Crash on close - offline mode
    * Crash during Offline Analysis
    * Crash reordering traces in Trace Options Widget
    * Crashes when Resubmitting twice in Offline Mode after Submitting in DAQ mode
    * Crash on Close with DAQ Tab
    * Crash when adding graphic plot when style is NULL
    * Crash on failed setup
    * Crash after failed licensing in RWX Reader
    * Offline Analysis Crashes on Submit when there are no Streams
    * DX+ crashes on failed setup
    * Crash with RWX Simulator and "Parameter" history plot
    * Crash in Start/Stop operations
    * Crash - DX+ Remote Viewer crashes without Crash Reporter when store unreachable
    * DX+ Viewer - Closing DX+ Receive - App becomes unresponsive
    * DX+ Viewer - DX+ Receive doesn't handle invalid URI
    * DX+ DAQ - Unable to submit design infinite loop with no timeout
  * Plot Management
    * Crash when opening old plot setup file
    * Crash when deleting Campbell plot
    * Crash when plotting too many signals
    * Offline Mode Crash when Placing Multiple-Traces on Plots
    * Axis Widget Causes Crash on some calls to Setup Axes
    * Load Pages Slider Crash
    * SQLInput Crash on old .dbs files
    * Datatel Crash
    * Crash when selecting Single Cursor on Campbell Plot
    * Crash when adjusting Campbell Z Axis Threshold too fast
    * Campbell Crashes on Color Phase mode after pressing delete
    * Crash when clicking clear all plots
    * Graphic Plot Element Right Click Plotsetup Crash
    * Plot Setups Crash DX+
    * Deleting Spectrum Plots Crashes Viewer
    * Viewer Crashes when switching
    * Removing Cells Reorders Plots + Crash
    * Crash when deleting Plot Page and Navigating to DAQControl Page
    * Crash when right-clicking on Plot Space After Plot Has Been Deleted
    * Crash when right-clicking on Datatel stream count or IP address
  * File Operations
    * Standalone Viewer crashes when plotting data from a changing SQLite file
    * Crash when switching to Viewer with no Viewer Element
  * Element Management
    * Copy/Paste Elements cause crash when connected
    * Paste crashes the designer
    * Deleting components doesn't delete properly
    * Stream Tags Ignore Disabled Elements causing crash
    * Crash when removing connection
    * Component Manager Sorting Issue Returns resulting in Invalid design
    * Rev Resample setting for PPR defaults to 0 until clicked
  * Application Lifecycle
    * Viewer becomes unresponsive and must be force quit
    * DX+ Crashing on Close
    * ALM crashes when applying demo license
    * ALM shuts down after install even after clicking no on installer dialog
    * Restart Button does not function in Crash Reporter
    * ALM Install first launch error

## 2024.39 (released 2024-09-30)

* Initial release of DX+

