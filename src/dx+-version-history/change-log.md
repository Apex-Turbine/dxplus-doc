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

## 2025.15 (released 2025-04-15)

* Updated Installer
  * Added ability to select individual devices, processors, outputs, etc. for installation
* Plotting Updates
  * Added Plot Selector Dialog
  * Added Signal vs. Signal capability for Time, History & Strip plots
* New Designer Elements
  * Input
    * Audio Input
    * Cyres Subscriber
    * Scanivavle Device
    * Apex-H5 (offline mode)
    * CADDMAS-H5 (offline mode)
  * Output
    * Apex-H5
* Updated Designer Elements
  * FFT & DFT elements have been combined
    * "Mode" option enables switching between FFT & DFT
  * Added Help tab to element settings panels to easily reference documentation about elements & API
* Fixed Bugs
  * Plot Functionality
    * Plot Auto Axis scaling not working
    * Ribbon Axis min/max doesn't allow large numbers
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
    * Subscriber DX can incorrectly stop/start Publisher DX
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
    * Crash when clicking Publisher output element after submitting design
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
  * Application Lifecycle
    * Viewer becomes unresponsive and must be force quit
    * DX+ Crashing on Close
    * ALM crashes when applying demo license
    * ALM shuts down after install even after clicking no on installer dialog
    * Restart Button does not function in Crash Reporter
    * ALM Install first launch error

## 2024.39 (released 2024-09-30)

* Initial release of DX+

