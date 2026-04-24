# PMT Calibration Procedure

This guide outlines the standard procedure for calibrating PMTs.

---

## Part 1: Hardware & Dark Box Setup

**1. Turn on the LED Source**
* Remember to wait 10-15 minutes for the light output to stabilize before proceeding to the next step.

**2. Ensure the High Voltage (HV) is Offline**
* **Software:** Send the CAEN power supply command `F11` (OFF).
* **Hardware:** Pull and push down the physical OFF switch on the power supply.

**3. Prepare the PMT in the Dark**
* Turn off the room's lights.
* Remove the black light-blocking sheet covering the dark box and open it.
* Verify that the PMT is properly connected to its socket.
* Place the PMT onto the support structure.
* Wrap and cover the socket with aluminum foil for shielding.

**4. Fix the PMT Position**
* With the PMT on the support, screw both top pieces of the support together to securely fix the PMT's position directly in front of the LED source.

**5. Connect the Cabling**
* Connect the HV cable to the HV port.
* Connect the BNC cable to the readout port.

**6. Seal the Dark Box**
* Remove the cover from the photocathode.
* Close the dark box.
* Cover the box completely with the black sheet to ensure it is completely light-tight.

---

## Part 2: Signal Verification

**7. Power Up and Check Pulses**
* Turn on the HV and **slowly** raise the voltage to `900V`.
* Log into the DAQ computer.
* In the browser page of the DAQ, navigate to the **Programs** tab and check that `CUPID NMV` is green. If it is not, press **Start**.
* In the **ODB** tab, verify that the sampling frequency is set to `2500` (2.5 Ms/s).
* Start a test data-taking run with the following settings:
  * **Write:** Unticked (Disabled)
  * **Number of events:** `-1`
* Open the **Event Viewer** from the terminal:
  * Navigate to the source folder by typing: `cd daq/online/source`
  * Launch the viewer: `python3 eventviewer.py -c 4` *(Note: check if the connected channel is N.4).*
* Check that the current channel is registering visible signal in the `650` to `750` samples range.

---

## Part 3: Single Photoelectron (SPE) Acquisition

**8. SPE Data Collection**
* Set the HV to `1100V`.
* Turn the wheel on the LED and align it between `0` and `0.2`. *(Note: Due to calibration offsets, these specific values are required to produce SPE).*
* Check the Event Viewer: The waveform should appear empty approximately 9 out of 10 times.
* Acquire `4000` events. (Use start run from DAQ page with Write data ticked)
* Run the analysis script: `runAnal.py` (it works on notebooks).
* Verify that the Trigger Rate is between **10% (0.10)** and **5% (0.05)**.
* Remember to write in the `PMT_characterisation\Datatake` file ( available at [Logbook_PMT](https://docs.google.com/spreadsheets/d/1_ymctPCSqQi_dhAj0rm1txnjqNDXYLwxiHr_jPbpXd8/edit?usp=sharing) ) the PMT ID, the monitored current and voltage and run number, in the same style as previously taken runs.
* **Voltage Sweep:** Once you have verified all of the points above, repeat this measurement, decreasing the voltage in steps of `50V`, all the way down to `950V` (i.e., 1050V, 1000V, 950V, etc.).

---

## Part 4: HIGH Intensity Mode Acquisition

**9. HIGH Mode Data Collection**
* Reset the HV back to `1100V`.
* Set the LED dial to approximately `3.6`.
* Check the Event Viewer: On average, the pulses should show a drop of about `2500` ADC counts from the baseline (down to roughly `1000` ADC counts).
  * *Tip: It is helpful to set a fixed top (`-t`) and bottom (`-b`) range in the Event Viewer to monitor this.*
* Adjust the LED power slightly up or down to match this average drop.
* Like in the SPE acquisition mode, all runs must be recored in the `PMT_characterisation\Datatake` file.
* **Voltage Sweep:** Repeat the measurements, decreasing the voltage in steps of `50V`, all the way down to `800V`.
