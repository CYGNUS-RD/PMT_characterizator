# PMT Calibration Procedure

This guide outlines the standard procedure for calibrating PMTs.

---

## Part 1: Hardware & Dark Box Setup

**1. Ensure the High Voltage (HV) is Offline**
* **Software:** Send the CAEN power supply command `F11` (OFF).
* **Hardware:** Pull and push down the physical OFF switch on the power supply.

**2. Prepare the PMT in the Dark**
* Turn off the room's lights.
* Remove the black light-blocking sheet covering the dark box and open it.
* Verify that the PMT is connected to its socket.
* Place the PMT onto the support structure.
* Wrap and cover the socket with aluminum foil for shielding.

**3. Fix the PMT Position**
* With the PMT on the support, screw both top pieces of the support together to securely fix the PMT's position in front of the LED source.

**4. Connect the Cabling**
* Connect the HV cable to the HV port in the box (note: the HV port is connected via the red cable to the HV module).
* Connect the BNC to the readout port.

**5. Seal the Dark Box**
* Remove the cover from the photocathode.
* Close the dark box.
* Cover the box completely with the black sheet to ensure it is light-tight.

---

## Part 2: Signal Verification

**6. Power Up and Check Pulses**
* Turn on the HV and **slowly** raise the voltage to `900V`.
* Log into the DAQ computer (Password: `daqwc`).
* Start a test data taking run with the following settings:
  * **Write:** Unticked (Disabled)
  * **Number of events:** `-1`
* Open the **Event Viewer** from terminal. Check that the current channel is registering visible spikes in the `650` to `750` samples range.

---

## Part 3: Single Photoelectron (SPE) Acquisition

**7. SPE Data Collection**
* Set the HV to `1100V`.
* Turn the wheel on the LED and align it between `0` and `0.2`. *(Note: Due to calibration offsets, these specific values are required to produce SPE).*
* Check the Event Viewer: The waveform should appear empty approximately 9 out of 10 times.
* Acquire `4000` events.
* Run the analysis script: `runAnal.py`.
* Verify that the Trigger Rate is between **10% (0.10)** and **5% (0.05)**.
* **Voltage Sweep:** Repeat this measurement, decreasing the voltage in steps of `50V`, all the way down to `800V` (i.e., 1050V, 1000V, 950V, etc.).

---

## Part 4: high intensity Mode Acquisition

**8. HIGH Mode Data Collection**
* Reset the HV back to `1100V`.
* Set the LED dial to approximately `3.6`.
* Check the Event Viewer: On average, the pulses should show a drop of about `2500` ADC counts from the baseline (down to roughly `1000` ADC counts).
  * *Tip: It is helpful to set a fixed top (`-t`) and bottom (`-b`) range in the Event Viewer to monitor this.*
* Adjust the LED power slightly up or down to match this average drop.
* **Voltage Sweep:** Repeat the measurements, decreasing the voltage in steps of `50V`, all the way down to `800V`.