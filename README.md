# PSOC&trade; 4: MSCLP low power self-capacitance touchpad with 4mm overlay

This code example demonstrates how to use the CAPSENSE&trade; middleware to detect a finger touch position on a self-capacitance-based touchpad widget in PSOC&trade; 4100T PLUS device with a 5th-generation low-power CAPSENSE™ (MSCLP).

In addition, this code example also explains how to manually tune the self-capacitance-based touchpad for optimum performance according to parameters such as reliability, power consumption, response time, and linearity using the CSD-RM sensing technique and CAPSENSE&trade; Tuner. Here, capacitive sigma-delta (CSD) represents the self-capacitance sensing technique and RM represents the ratiometric method.

[View this README on GitHub.](https://github.com/Infineon/mtb-example-psoc4-msclp-low-power-csd-touchpad-4mm-overlay)

[Provide feedback on this code example.](https://cypress.co1.qualtrics.com/jfe/form/SV_1NTns53sK2yiljn?Q_EED=eyJVbmlxdWUgRG9jIElkIjoiQ0UyNDA1NTYiLCJTcGVjIE51bWJlciI6IjAwMi00MDU1NiIsIkRvYyBUaXRsZSI6IlBTT0MmdHJhZGU7IDQ6IE1TQ0xQIGxvdyBwb3dlciBzZWxmLWNhcGFjaXRhbmNlIHRvdWNocGFkIHdpdGggNG1tIG92ZXJsYXkiLCJyaWQiOiJsdWNreSIsIkRvYyB2ZXJzaW9uIjoiMy4wLjAiLCJEb2MgTGFuZ3VhZ2UiOiJFbmdsaXNoIiwiRG9jIERpdmlzaW9uIjoiTUNEIiwiRG9jIEJVIjoiSUNXIiwiRG9jIEZhbWlseSI6IlBTT0MifQ==)

## Requirements

- [ModusToolbox&trade;](https://www.infineon.com/modustoolbox) v3.5 or later

- Board support package (BSP) minimum required version: 3.3.0
- Programming language: C
- Associated parts: [PSOC&trade; 4100T PLUS](https://www.infineon.com/002-39671)

## Supported toolchains (make variable 'TOOLCHAIN')

- GNU Arm&reg; Embedded Compiler v11.3.1 (`GCC_ARM`) – Default value of `TOOLCHAIN`
- Arm&reg; Compiler v6.22 (`ARM`)
- IAR C/C++ Compiler v9.50.2 (`IAR`)

## Supported kits (make variable 'TARGET')

- [PSOC&trade; 4100T PLUS CAPSENSE&trade; Prototyping kit](https://www.infineon.com/CY8CPROTO-041TP) (`CY8CPROTO-041TP`) – Default value of `TARGET`

## Hardware setup
To evaluate touchpad operation with 4mm overlay mount the supplied 3mm add-on overlay on top of 1mm overlay over the touchpad wing.

This example uses the board's default configuration. See the kit user guide to configure the required operating voltage on the kit and to setup the VDDA supply voltage refer to section [Set up the VDDA supply voltage and debug mode in Device Configurator](#set-up-the-vdda-supply-voltage-and-debug-mode-in-device-configurator).

This application is tuned to perform optimally at the default voltage. However, you can observe the basic functionality at other supported voltages.

**Table 1. Kit user guide and supporting voltages**

   Kit | User guide  | 1.8V | 3.3V | 5V
   :-------- |:----------- |:----------- |:----- |:-----
   [CY8CPROTO-041TP](https://www.infineon.com/CY8CPROTO-041TP) | [PSOC&trade; 4100T Plus CAPSENSE&trade; Prototyping Kit guide](https://www.infineon.com/002-40273) | Yes | Yes | Yes*


Yes* - Kit default operating voltage

## Software setup

See the [ModusToolbox&trade; tools package installation guide](https://www.infineon.com/ModusToolboxInstallguide) for information about installing and configuring the tools package.

This example requires no additional software or tools.


## Using the code example

### Create the project

The ModusToolbox&trade; tools package provides the Project Creator as both a GUI tool and a command line tool.

<details><summary><b>Use Project Creator GUI</b></summary>

1. Open the Project Creator GUI tool.

   There are several ways to do this, including launching it from the dashboard or from inside the Eclipse IDE. For more details, see the [Project Creator user guide](https://www.infineon.com/ModusToolboxProjectCreator) (locally available at *{ModusToolbox&trade; install directory}/tools_{version}/project-creator/docs/project-creator.pdf*).

2. On the **Choose Board Support Package (BSP)** page, select a kit supported by this code example. See [Supported kits](#supported-kits-make-variable-target).

   > **Note:** To use this code example for a kit not listed here, you may need to update the source files. If the kit does not have the required resources, the application may not work.

3. On the **Select Application** page:

   a. Select the **Applications(s) Root Path** and the **Target IDE**.

   > **Note:** Depending on how you open the Project Creator tool, these fields may be pre-selected for you.

   b.	Select this code example from the list by enabling its check box.

   > **Note:** You can narrow the list of displayed examples by typing in the filter box.

   c. (Optional) Change the suggested **New Application Name** and **New BSP Name**.

   d. Click **Create** to complete the application creation process.

</details>

<details><summary><b>Use Project Creator CLI</b></summary>

The 'project-creator-cli' tool can be used to create applications from a CLI terminal or from within batch files or shell scripts. This tool is available in the *{ModusToolbox&trade; install directory}/tools_{version}/project-creator/* directory.

Use a CLI terminal to invoke the 'project-creator-cli' tool. On Windows, use the command-line 'modus-shell' program provided in the ModusToolbox&trade; installation instead of a standard Windows command-line application. This shell provides access to all ModusToolbox&trade; tools. You can access it by typing "modus-shell" in the search box in the Windows menu. In Linux and macOS, you can use any terminal application.

The following example clones the "mtb-example-psoc4-msclp-low-power-csd-touchpad" application with the desired name "MSCLPlowpowerSelfCapTouchpad" configured for the *CY8CPROTO-041TP* BSP into the specified working directory, *C:/mtb_projects*:

   ```
   project-creator-cli --board-id CY8CPROTO-041TP --app-id mtb-example-psoc4-msclp-low-power-self-capacitance-touchpad --user-app-name MSCLPSelfCapTouchpadTuning --target-dir "C:/mtb_projects"
   ```


The 'project-creator-cli' tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--board-id` | Defined in the <id> field of the [BSP](https://github.com/Infineon?q=bsp-manifest&type=&language=&sort=) manifest | Required
`--app-id`   | Defined in the <id> field of the [CE](https://github.com/Infineon?q=ce-manifest&type=&language=&sort=) manifest | Required
`--target-dir`| Specify the directory in which the application is to be created if you prefer not to use the default current working directory | Optional
`--user-app-name`| Specify the name of the application if you prefer to have a name other than the example's default name | Optional

> **Note:** The project-creator-cli tool uses the `git clone` and `make getlibs` commands to fetch the repository and import the required libraries. For details, see the "Project creator tools" section of the [ModusToolbox&trade; tools package user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at {ModusToolbox&trade; install directory}/docs_{version}/mtb_user_guide.pdf).

</details>



### Open the project

After the project has been created, you can open it in your preferred development environment.


<details><summary><b>Eclipse IDE</b></summary>

If you opened the Project Creator tool from the included Eclipse IDE, the project will open in Eclipse automatically.

For more details, see the [Eclipse IDE for ModusToolbox&trade; user guide](https://www.infineon.com/MTBEclipseIDEUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mt_ide_user_guide.pdf*).

</details>


<details><summary><b>Visual Studio (VS) Code</b></summary>

Launch VS Code manually, and then open the generated *{project-name}.code-workspace* file located in the project directory.

For more details, see the [Visual Studio Code for ModusToolbox&trade; user guide](https://www.infineon.com/MTBVSCodeUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mt_vscode_user_guide.pdf*).

</details>


<details><summary><b>Keil µVision</b></summary>

Double-click the generated *{project-name}.cprj* file to launch the Keil µVision IDE.

For more details, see the [Keil µVision for ModusToolbox&trade; user guide](https://www.infineon.com/MTBuVisionUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mt_uvision_user_guide.pdf*).

</details>


<details><summary><b>IAR Embedded Workbench</b></summary>

Open IAR Embedded Workbench manually, and create a new project. Then select the generated *{project-name}.ipcf* file located in the project directory.

For more details, see the [IAR Embedded Workbench for ModusToolbox&trade; user guide](https://www.infineon.com/MTBIARUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mt_iar_user_guide.pdf*).

</details>


<details><summary><b>Command line</b></summary>

If you prefer to use the CLI, open the appropriate terminal, and navigate to the project directory. On Windows, use the command-line 'modus-shell' program; on Linux and macOS, you can use any terminal application. From there, you can run various `make` commands.

For more details, see the [ModusToolbox&trade; tools package user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mtb_user_guide.pdf*).

</details>



## Operation


1. Connect the board to your PC using the provided cable through the KitProg3 USB connector.

2. Program the board using one of the following:

   <details><summary><b>Using Eclipse IDE</b></summary>

      1. Select the application project in the Project Explorer.

      2. In the **Quick Panel**, scroll down, and click **\<Application Name> Program (KitProg3_MiniProg4)**.
   </details>


   <details><summary><b>In other IDEs</b></summary>

   Follow the instructions in your preferred IDE.
   </details>


   <details><summary><b>Using CLI</b></summary>

     From the terminal, execute the `make program` command to build and program the application using the default toolchain to the default target. The default toolchain is specified in the application's Makefile but you can override this value manually:
      ```
      make program TOOLCHAIN=<toolchain>
      ```

      Example:
      ```
      make program TOOLCHAIN=GCC_ARM
      ```
   </details>

3. After programming, the application starts automatically.

   > **Note:** After programming, you may see the following error message if debug mode is disabled, see Table 14 for the default debug configuration in the supported kits. Ignore the error or enable the debug mode to solve this error.

   ``` c
   "Error: Error connecting Dp: Cannot read IDR"
   ```

4. To test the application, slide your finger over the CAPSENSE&trade; touchpad and notice that the LED mentioned in **Table 2** turns ON when touched and turns OFF when the finger is lifted.

   **Table 2. LED indications**

   Scenario  | CY8CPROTO-041TP |  Status
   :------------------| :-----| :-----
   Touch (Column)  | LED3 | Brightness increases when the finger is swiped from left to right
   Touch (Row) | LED2  |Brightness increases when the finger is swiped from bottom to top

5. You can also monitor the CAPSENSE&trade; data using the CAPSENSE&trade; Tuner application as follows:

    **Monitor data using CAPSENSE&trade; Tuner**

    1. Open CAPSENSE&trade; Tuner from the tools section in the IDE **Quick Panel**.

        You can also run the CAPSENSE&trade; Tuner application in standalone mode from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/capsense-configurator/capsense-tuner*. In this case, after opening the application, select **File** > **Open** and open the *design.cycapsense* file of the respective application, which is present in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/config/* folder.

	 See the [ModusToolbox&trade; user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at {*ModusToolbox&trade; install directory}/docs_{version}/mtb_user_guide.pdf*) for options to open the CAPSENSE&trade; Tuner application using the CLI.

    2. Ensure the kit is in CMSIS-DAP bulk mode (KitProg3 status LED is ON and not blinking). See [Firmware-loader](https://github.com/Infineon/Firmware-loader) to learn how to update the firmware and switch modes in KitProg3.

    3. In the tuner application, click on the **Tuner Communication Setup** icon or select **Tools** > **Tuner Communication Setup**. In the window, select I2C under KitProg3 and configure as follows:

         - **I2C address:** 8
         - **Sub-address:** 2-Bytes
         - **Speed (kHz):** 400

         These are the same values set in the EZI2C resource.

      **Figure 1. Tuner Communication Setup parameters**

      <img src="images/tuner-comm-setup.png" alt="Figure 1" width="600" />

6. Click **Connect** or select **Communication** > **Connect** to establish a connection.

   **Figure 2. Establish a connection**

   <img src="images/tuner-connect.png" alt="Figure 2" width="400" />

7. Click **Start** or select **Communication** > **Start** to start data streaming from the device.

   **Figure 3. Start tuner communication**

   <img src="images/tuner-start.png" alt="Figure 3" width="400" />

   The tuner displays the data from the sensor in the **Widget View**, **Graph View**, and **Touchpad View** tabs.

8. Set the **Read mode** to **Synchronized** mode. Navigate to the **Widget View** tab and observe that the **TOUCHPAD_SELF_CAP** widget is highlighted in blue color when you touch it.

   **Figure 4. Widget view of the CAPSENSE&trade; Tuner**

   <img src="images/widget-view.png" alt="Figure 4" width="800"/>

9. You can view the raw count, baseline, difference count, status for each sensor, and touchpad position in the **Graph View** tab. For example, to view the sensor data for TOUCHPAD_SELF_CAP, select **TOUCHPAD_SELF_CAP_Col0** under **TOUCHPAD_SELF_CAP**.

   **Figure 5. Graph View tab of the CAPSENSE&trade; Tuner**

   <img src="images/graph_view.png" alt="Figure 5" width="800"/>

10. The **Touchpad View** tab shows the heatmap view and the finger movement can be visualized on the same.

      **Figure 6. Touchpad view of the CAPSENSE&trade; Tuner**

      <img src="images/touchpad-view.png" alt="Figure 6" width="800"/>

11. See the **Widget/Sensor Parameters** section in the CAPSENSE&trade; Tuner window. The configuration parameters for each touchpad sensor element calculated by the CAPSENSE&trade; resource are displayed as shown in **Figure 6**.

12. Verify that the signal-to-noise ratio (SNR) is greater than 5:1 and the signal count is above 50 by following the steps given in [Stage 4:  Obtain noise and crossover point](#stage-3-obtain-noise-and-crossover-point).

Non-reporting of false touches and the linearity of the position graph indicate proper tuning.

> **Note:** Refer to the PSOC&trade; 4: MSCLP low-power CSD button CE to observe the power state transitions, Measure current at different power modes section. The Code Example also explains the scan time and process time measurements.

</details>

## Tuning procedure

### Create custom BSP for your board

1. Create a custom BSP for your board with any device by following the steps given in [ModusToolbox&trade; BSP Assistant user guide](https://www.infineon.com/ModusToolboxBSPAssistant). 

2. Open the *design.modus* file from the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/config/* folder obtained in the previous step and enable CAPSENSE&trade; to get the *design.cycapsense* file. CAPSENSE&trade; configuration can be started from scratch as follows:

The following steps explain the tuning procedure.

> **Note:** See the "Selecting CAPSENSE&trade; hardware parameters" section in the [PSOC&trade; 4 and PSOC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951) to learn about the considerations for selecting each parameter value.

The tuning flow of the proximity widget is shown in **Figure 7**.

**Figure 7. CSD touchpad widget tuning flow**

<img src="images/flowchart_for_tuning.png" alt="Figure 7" width="500" />

Do the following to tune the touchpad widget:

- [Stage 1: Set the initial hardware parameters](#stage-1-set-the-initial-hardware-parameters)

- [Stage 2: Set the sense clock frequency](#stage-2-set-the-sense-clock-frequency)

- [Stage 3: Measure sensor capacitance to set CDAC tuning mode](#stage-3-measure-sensor-capacitance-to-set-cdac-tuning-mode)

- [Stage 4: Obtain noise and crossover point](#stage-4-obtain-noise-and-crossover-point)

- [Stage 5: Fine-tune sensitivity to improve SNR](#stage-5-fine-tune-sensitivity-to-improve-snr)

- [Stage 6: Tune threshold parameters](#stage-6-tune-threshold-parameters)


### Stage 1: Set the initial hardware parameters
------------

1. Connect the board to your PC using a USB cable through the KitProg3 USB connector.

2. Launch the Device Configurator tool.

   You can launch the Device Configurator in Eclipse IDE for ModusToolbox&trade; from the **BSP Configurators** section in the IDE **Quick Panel** or in standalone mode from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/device-configurator/device-configurator*. In this case, after opening the application, select **File** > **Open** and open the *design.modus* file of the respective application located in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/config/* folder.

3. In the [PSOC&trade; 4100T Plus kit](https://www.infineon.com/CY8CPROTO-041TP), the touchpad pins are connected to CAPSENSE&trade; channel (MSCLP 0). Therefore, ensure that you enable CAPSENSE&trade; channel in the **Device Configurator** as shown in **Figure 8**.

   **Figure 8. Enable MSCLP channel in the Device Configurator**

   <img src="images/device-configurator-channel.png" alt="Figure 8" width="800"/>

   Save the changes and close the window.

4. Launch the CAPSENSE&trade; Configurator tool.

   You can launch the CAPSENSE&trade; Configurator tool in the Eclipse IDE from the CAPSENSE&trade; **Peripherals** tab in the Device Configurator or directly from the **Tools** section in the IDE **Quick Panel**. You can also launch it in standalone mode from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/capsense-configurator/capsense-configurator*. In this case, after opening the application, select **File** > **Open** and open the *design.cycapsense* file of the respective application located in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/config/* folder.

   See the [ModusToolbox&trade; CAPSENSE&trade; Configurator tool guide](https://www.infineon.com/ModusToolboxCapSenseConfig) for step-by-step instructions on how to configure and launch CAPSENSE&trade; in ModusToolbox&trade;.

5. In the **Basic** tab, note that a single touchpad, **TOUCHPAD_SELF_CAP** is configured with CSD RM (self-cap) Sensing Mode.

   **Figure 9. CAPSENSE&trade; Configurator - Basic tab**

   <img src="images/capsense_basictab.png" alt="Figure 9" width="800"/>

6. Go to **Advanced** > **General** tab and do the following:

   **Table 3. Widget details**

   Parameter | Setting | Comment
   :-------- |:----------- |:-----------
   CAPSENSE&trade; IMO Clock frequency (MHz) | 46 | Frequency of clock used as source for the CAPSENSE™ peripheral
   Modulator clock divider | 1 | Set to obtain the optimum modulator clock frequency
   Number of init sub-conversions | 3 | Set to ensure proper initialization of CAPSENSE™.

   > **Note:** Retain the default settings for all regular and low-power widget filters. You can enable or update the filters later depending on the signal-to-noise ratio (SNR) requirements in [Stage 5: Fine-tune for required SNR, power, and refresh rate](#stage-3-obtain-noise-and-crossover-point).

      Filters are used to reduce the peak-to-peak noise; however, using filters will result in a higher scan time.

   **Figure 10. CAPSENSE&trade; Configurator – General settings**

   <img src="images/adv_general.png" alt="Figure 10" width="800"/>

   > **Note:** Each tab has a **Restore Defaults** button to restore the parameters of that tab to their default values.

7. Go to **CSD Settings** tab and make the following changes:

   **Table 4. Scan setting**

   Parameter | CY8CPROTO-041TP |Comment
   :-------- |:-----------  |:-----------
   Inactive sensor connection | Shield | Connects the inactive sensors ( configured sensors which are not  scanned in a given scan-slot ) to the driven shield.
   Shield mode | Active | The driven shield is a signal that replicates the sensor-switching signal. It helps to reduce sensor parasitic capacitance.  
   Total shield count | 2 |  Selects the number of shield electrodes used in the design. Most designs work with one dedicated shield electrode, but some designs require multiple dedicated shield electrodes to ease the PCB layout routing or to minimize the PCB area used for the shield layer.
   Raw count calibration level (%) | 85 | If the sensor raw count saturates (equals Max Raw count) on touch, reduce the Raw count calibration level(%). which helps in avoiding saturation

   **Figure 11. CAPSENSE&trade; Configurator – Advanced CSD settings**

   <img src="images/csd_advanced.png" alt="Figure 11" width="800"/>

8. Go to the **Widget Details** tab. Select **TOUCHPAD_SELF_CAP** from the left pane and then set the following:

   **Table 5. Initial widget parameter setting**

   Parameter | Setting | Comment
   :-------- |:----------- |:-----------
   Maximum X-Axis position| 255 | A touch on touchpad produces a position value from 0 to Maximum X-Axis position
   Maximum Y-Axis position | 255 | A touch on touchpad produces a position value from 0 to Maximum Y-Axis position
   Column sense clock divider | Default | Value will be set in [Stage 2:  Set sense clock frequency](#stage-2-set-the-sense-clock-frequency)
   Row sense clock divider | Default | Value will be set in [Stage 2:  Set sense clock frequency](#stage-2-set-the-sense-clock-frequency)
   Clock source |Direct | Direct clock is a constant frequency sense clock source. When you chose this option, the sensor pin switches with a constant frequency.
   Number of sub-conversions | 12 | Good starting point to ensure a fast scan time and sufficient signal. This value will be adjusted as required in [Stage 5: Fine-tune for required SNR, power, and refresh rate](#stage-3-obtain-noise-and-crossover-point)
   Finger threshold | 20 |It is initially set to a low value which allows the **Touchpad View** to track the finger movement during tuning
   Noise threshold |10 |Baseline is not updated when raw count is above baseline + Noise threshold.
   Negative noise threshold |10 |Baseline is not updated when raw count is below baseline - Negative noise threshold.
   Hysteresis | 5 |Prevents sensor status toggling due to system noise.
   ON debounce | 3 |Number of consecutive scans during which a sensor must be active so that a touch is reported.

   These values reduce the influence of the baseline on the sensor signal which helps to get the true difference count. Retain the default values for all other threshold parameters; these parameters are set in [Stage 6: Tune threshold parameters](#stage-5-tune-threshold-parameters).

   **Figure 12. CAPSENSE&trade; Configurator - Widget Details settings**

   <img src="images/adv_widget_detail.png" alt="Figure 12" width="800" />

9. To select pins and scan slots, go to **Scan Configuration** tab and do the following:

   **Figure 13. Scan Configuration tab**

   <img src="images/scan-configuration.png" alt="Figure 13" width="800"/>

   1. Configure pins for the electrodes using the drop-down menu.

   2. Configure the scan slots using **Auto-Assign Slots** option.It will automatically reassigns all slots for sensors based on a widget and sensor order.

   3. Check the notice list for warnings or errors.

      > **Note:** Enable the **Notice List** from the **View** menu if the notice list is not visible.

10. Click **Save** to apply the settings.

See the [CAPSENSE&trade; design guide](https://www.infineon.com/AN85951) for detailed information on tuning parameters.


### Stage 2: Set the sense clock frequency
-----------------

The sense clock is derived from the modulator clock using a sense clock-divider and is used to scan the sensor by driving the CAPSENSE&trade; switched-capacitor circuits. Both the clock source and clock divider are configurable. The sense clock divider should be configured such that the pulse width of the sense clock is long enough to allow the sensor capacitance to charge and discharge completely. This is verified by observing the charging and discharging waveforms of the sensor using an oscilloscope and an active probe. The sensors should be probed close to the electrode and not at the sense pins or the series resistor. 

See **Figure 14** and **Figure 15** for waveforms observed on the shield. **Figure 14** shows proper charging when the sense clock frequency is correctly tuned. The pulse width is at least 5 Tau, i.e., the voltage is reaching at least 99.3% of the required voltage at the end of each phase. **Figure 15** shows incomplete settling (charging/discharging).


**Figure 14. Proper charge cycle of a sensor**

<img src="images/csdrm-waveform.png" alt="Figure 14" width="400"/>



**Figure 15. Improper charge cycle of a sensor**

<img src="images/csdrm-waveform-improper.png" alt="Figure 15" width="400"/>

1. Program the board and launch CAPSENSE&trade; Tuner.

2. See the charging waveform of the sensor as described earlier. 

3. If the charging is incomplete, increase the sense clock divider. Do this in CAPSENSE&trade; Tuner by selecting the sensor and editing the sense clock divider parameter in the Widget/Sensor Parameters panel.

    > **Note:** The sense clock divider should be **divisible by 4**. This ensures that all four scan phases have equal durations. 

   After editing the value, click the **Apply to Device** button and observe the waveform again. Repeat this until complete settling is observed. Using a passive probe will add an additional parasitic capacitance of around 15 pF; therefore, should be considered during the tuning. 
   
4. Click the **Apply to Project** button so that the configuration is saved to your project. 

   **Figure 16. Sense clock divider setting**

   <img src="images/sense_clock_divider_setting.png" alt="Figure 16" width="400" />
   

5. Repeat this process for all the sensors and the shield. Each sensor may require a different sense clock divider value to charge/discharge completely. But all the sensors that are in the same scan slot need to have the same sense clock source, sense clock divider, and number of sub-conversions. Therefore, take the largest sense clock divider in a given scan slot and apply it to all the other sensors that share that slot.

**Table 6. Sense clock divider settings obtained for supported kits**

   Parameter |CY8CPROTO-041TP
   :-------- |:----------- 
   Sense clock divider | 24  


### **Stage 3: Measure sensor capacitance to set CDAC tuning mode**
------------

Generally CDAC tuning mode is recommended to be set to Auto, however the appropriate tuning mode to use has some dependency on the sensor parasitic capacitance (Cp).
 
 
In order to avoid signal variation across devices in production, PSOC 4100T Plus devices have CDAC trim codes in SFLASH (read-only). This code is used to scale the Reference CDAC and Fine CDAC parameters, which compensates for variations in the CDAC and brings down the overall signal variation across units.

This trimming is applicable only in the following scenarios,
- Only for CSD widgets (Regular and Low power).
- Sensor Cp is less than 4pF.
- Reference CDAC and Fine CDAC are set to 'Manual' mode.


   >   **Note:** 
   Select CDAC tuning mode 'Auto', if sensor Cp is above 4pF. Also for sensing methods other than CSD.

>  **Note:** To determine the applicable CDAC tuning mode for configuration in this code example, measure the sensor parasitic capacitance (Cp). If Cp is less than 4pF, reference CDAC and fine CDAC should be configured to 'Manual' mode. Refer to the [PSOC&trade; 4: MSCLP low power self-capacitance touchpad](https://github.com/Infineon/mtb-example-psoc4-msclp-low-power-csd-touchpad) code example for the procedure to measure Cp and for the steps to configure the CDACs manually.


### Stage 4: Obtain noise and crossover point 
---------------

To obtain the noise and crossover point, do the following:

1. Program the board.

2.  Launch the CAPSENSE&trade; Tuner to monitor the CAPSENSE&trade; data and for CAPSENSE&trade; parameter tuning and SNR measurement.

    See the [CAPSENSE&trade; Tuner guide](https://www.infineon.com/ModusToolboxCapSenseTuner) for step-by-step instructions on how to launch and configure the CAPSENSE&trade; Tuner in ModusToolbox&trade;.


3. Capture the raw counts of each sensor element in the touchpad as shown in **Figure 17** and verify that they are approximately equal to 85% (± 5%) of the MaxCount. See [AN234231 - PSoC™ 4 CAPSENSE™ ultra-low-power capacitive sensing techniques](https://www.infineon.com/AN234231) for the MaxCount equation.

   1. Go to the **Touchpad View** tab and change the **Display settings** as follows:

      **Table 7. Display settings**

      Parameter | Setting | 
      :-------- |:----------- 
      Display mode | Touch reporting 
      Data type | RawCount
      Value type| Current
      Number of samples | 1000

      **Note:** Under Widget selection, enable Flip X-axis for proper visualization of finger movement on the touchpad.

   **Figure 17. Raw counts obtained on the Touchpad View tab in the Tuner window**

   <img src="images/touchpad-view-rc.png" alt="Figure 17" width="800"/>

4. Observe and note the peak-to-peak noise of each sensor element in the touchpad.

   1. Go to the **Touchpad View** tab and change the **Display settings** as follows:

      **Table 8. Display settings**

         Parameter | Setting | 
         :-------- |:----------- 
         Display mode | Touch reporting 
         Data type | RawCount
         Value type| Max-Min
         Number of samples | 1000

   **Figure 18. Noise obtained on the Touchpad View tab in the Tuner window**

   <img src="images/touchpad-view-noise.png" alt="Figure 18" width="800" />


      See the row and column having the highest raw counts without placing a finger (which gives the peak-to-peak noise) in the **Touchpad View**.
      
   2. Capture the accurate noise by following these steps: 

      a) Click on the highest value observed in the heatmap for Row.

      b) Click on **SNR Measurement** tab.

      c) Click on **Acquire Noise**.

      d) Repeat the above steps for the column as well.

     **Figure 19. Row noise obtained on the SNR Measurement tab in Tuner window**

    <img src="images/row-snr-noise.png" alt="Figure 19" width="800"/>

    

    **Figure 20. Column noise obtained on the SNR Measurement tab in Tuner window**

    <img src="images/column-snr-noise.png" alt="Figure 20" width="800"/>
   
   

   **Table 9. Maximum peak-to-peak noise obtained in supported kits**

   Kit | Maximum peak-to-peak noise for row sensors| Maximum peak-to-peak noise for column sensors
   :----------|:-------------------------| :------
   CY8CPROTO-041TP   | 103 | 118 
   
   <br>
   
5. Observe the sensor signal in the **Graph View** tab in the **Sensor Signal** graph display.

   a) Select the columns in **Widget Explorer** as shown in **Figure 21**. 
   
   b) Firmly swipe the finger (6 mm) horizontally on the touchpad in the **least touch intensity (LTI)** position.<br>Note the lowest crossover point observed under **Sensor Signal**.

   c) Repeat the above steps for row by swiping the finger vertically on the touchpad in the LTI position.

   > **Note:** The LTI signal is measured at the farthest point (not at the last column/row) of the touchpad from the sensor pin connection, where the sensors have the worst case RC-time constant.

   **Figure 21. Column signal obtained on the Graph View tab in Tuner window**

    <img src="images/column-signal.png" alt="Figure 21" width="800"/>
    
    

    **Figure 22. Row signal obtained on the Graph View tab in Tuner window**

    <img src="images/row-signal.png" alt="Figure 22" width="800"/>
   
   **Table 10. Sensor signal obtained in supported kits**

   Kit | LTI signal for row sensors| LTI signal for column sensors
   :----------|:-------------------------| :------
   CY8CPROTO-041TP   | 960 | 950
 
 <br>

### Stage 5: Fine-tune sensitivity to improve SNR
------------------

The CAPSENSE&trade; system may be required to work reliably in adverse conditions, such as a noisy environment. The touchpad sensors need to be tuned with SNR greater than 5:1 to avoid triggering false touches and to make sure that all intended touches are registered in these adverse conditions.

> **Note:** For gesture detection, it is recommended to have around 10:1 SNR.

1. Ensure that the LTI signal count is greater than 50 and meets at least 5:1 SNR (using **Equation 1**).

   In CAPSENSE&trade; Tuner window, increase the **Number of sub-conversions** (located in **Widget Hardware Parameters** > **Widget/Sensor Parameters** section) by **10** until you achieve at least 5:1 SNR.

   **Equation 1. SNR**

   ![](images/snr-equation.png)

   Where,

   - LTI signal is the signal obtained as shown in **Figure 21** and **Figure 22**

   - Pk-Pk noise is the peak-to-peak noise obtained as shown in **Figure 18**

   SNR is measured for row sensors and column sensors separately, using **Equation 1**.

   From the values derived from figures mentioned earlier, an example SNR calculation can be calculated as:

   SNR of column sensors = 885/118 = 7.5; SNR of row sensors = 923/103 = 8.9.

2. Update the number of sub-conversions.

   1. Update the **Number of sub-conversions (Nsub)** directly in the **Widget/Sensor parameters** tab of the CAPSENSE&trade; Tuner.

   2. PSOC&trade; 4 CAPSENSE&trade; devices with MSCLP have a built-in CIC2 filter. Enabling the CIC2 filter increases the resolution while maintaining the same scan time. See [AN234231 - PSoC™ 4 CAPSENSE™ ultra-low-power capacitive sensing techniques](https://www.infineon.com/AN234231) for detailed information on the CIC2 filter.
   Enable the other filters based on the type of noise in your system. For Filter Descriptions refer to **Table 11**.

       **Table 11. Filters Description**

      Filter   | Description
      :---------------------| :----------------- 
      Median  | Eliminates noise spikes from motors and switching power supplies
      Average  | Eliminates periodic noise (for example, from power supplies)
      First Order IIR | Software IIR filter which eliminates high frequency Noise, Low coefficient results in lower noise but slows down response. 
      Hardware IIR | Eliminates high frequency Noise, Low coefficient means lower filtering, while higher response time.




   3. Current consumption is directly proportional to the number of sub-conversions; therefore, decrease the number of sub-conversions to achieve lower current consumption.

      > **Note:** The number of sub-conversions should be greater than or equal to 8, and they should not be increased beyond a certain limit such that the raw count does not increase more than 2<sup>16</sup> (as it is a 16-bit counter).

3. After changing the **Number of sub-conversions**, click **Apply to Device** to send the setting to the device. The change is reflected in the graphs.

   > **Note:** 
   - The **Apply to Device** option is enabled only when the **Number of sub-conversions** is changed.
   - Decrease the IIR filter coefficient if 5:1 SNR is not being achieved even with maximum Nsub.


### Stage 6: Tune threshold parameters
---------------

After confirming that your design meets the timing parameters and the SNR is greater than 5:1, set your threshold parameters.

> **Note:** Thresholds are set based on the LTI position because it is the least valid touch signal that can be obtained.

1. Set the recommended threshold values mentioned in **Table 12** for the touchpad widget using the LTI signal value obtained in [Stage 5: Fine-tune sensitivity to improve SNR](#stage-4-fine-tune-sensitivity-to-improve-snr).

   **Table 12. Software tuning parameters obtained** 

      Parameter  | CY8CPROTO-041TP  |  Remark
      :---------------------| :-----| :-----|
      Number of sub-conversions	| 56|-
      Finger threshold |  760 |80% of the lower LTI signal (either Row or Column) |
      Noise threshold  | 380 | Twice the highest noise or 40% of the lower LTI signal (whichever is greater) |
      Negative noise threshold | 380 | Twice the highest noise or 40% of the lower LTI signal (whichever is greater) |
      Hysteresis  | 76 | 10% of the lower LTI signal  |
      Low baseline reset  | 30 | 30 (by default) | 
      ON debounce	| 3 | Default 

<br>

### Apply the settings to the firmware

Click **Apply to Device** and **Apply to Project** in the CAPSENSE&trade; Tuner window to apply the settings to the device and project respectively. Close the tuner.

   **Figure 23. Apply to project**

   <img src="images/apply_to_project.png" alt="Figure 23" width="400" />

   The change is updated in the *design.cycapsense* file and reflected in the CAPSENSE&trade; Configurator.

<br>

## Debugging

You can debug this project to step through the code. In the IDE, use the **\<Application Name> Debug (KitProg3_MiniProg4)** configuration in the **Quick Panel**. For details, see the "Program and debug" section in the [Eclipse IDE for ModusToolbox&trade; user guide](https://www.infineon.com/MTBEclipseIDEUserGuide).

To enable the debug option, see the [Setup VDDA and Debug mode](#set-up-the-vdda-supply-voltage-and-debug-mode-in-device-configurator) section. To achieve lower power consumption, it is recommended to disable it when not debugging.

see, **Table 13** for the default debug configuration in the supported kits,

**Table 13. Debug mode option status**

   Kit  | Debug mode 
   :----| :----------
   CY8CPROTO-041TP | Enabled


## Design and implementation

The project contains a touchpad widget configured in CSD-RM Sensing mode. See the [Tuning procedure](#tuning-procedure) section for step-by-step instructions to configure the other settings of the CAPSENSE&trade; Configurator.

The project uses the [CAPSENSE&trade; middleware](https://github.com/Infineon/capsense) (see ModusToolbox&trade; user guide for more details on selecting a middleware). See [AN85951 – PSOC&trade; 4 and PSOC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951) for more details on CAPSENSE&trade; features and usage.

[ModusToolbox&trade;](https://www.infineon.com/modustoolbox) provides a GUI-based tuner application for debugging and tuning the CAPSENSE&trade; system. The CAPSENSE&trade; Tuner application works with EZI2C and UART communication interfaces. This project has an SCB block configured in EZI2C mode to establish communication with the onboard KitProg, which in turn enables reading the CAPSENSE&trade; raw data by the CAPSENSE&trade; Tuner; see **Figure 26**.

The CAPSENSE&trade; data structure that contains the CAPSENSE&trade; raw data is exposed to the CAPSENSE&trade; Tuner by setting up the I2C communication data buffer with the CAPSENSE&trade; data structure. This enables the tuner to access the CAPSENSE&trade; raw data for tuning and debugging CAPSENSE&trade;.

The successful tuning of the touchpad is indicated by the user LED in the Prototyping; the LED3 brightness increases when the finger is swiped from left to right, and the LED2 brightness increases when the finger is swiped from bottom to top on the touchpad.


### Set up the VDDA supply voltage and debug mode in Device Configurator

1. Open Device Configurator from the **Quick Panel**.

2. Go to the **System** tab. Select the **Power** resource and set the VDDA value under **Operating Conditions** as shown in **Figure 24**.

   **Figure 24. Setting the VDDA supply in the System tab of Device Configurator**

   <img src="images/vdda-settings.png" alt="Figure 24" width="800"/>

3. See Table 14 for the default debug configuration in the supported kits. Enable the debug mode to enable the SWD pins as shown in **Figure 25**.

   **Figure 25. Enable debug mode in the System tab of Device Configurator**

   <img src="images/enable_debug.png" alt="Figure 25" width="800"/>



### Resources and settings

**Figure 26. EZI2C settings**

<img src="images/ezi2c-config.png" alt="Figure 26" width="800"/>



**Figure 27. PWM settings**

<img src="images/pwm-settings.png" alt="Figure 27" width="800" />




**Table 14. Application resources**

 Resource  |  Alias/object     |    Purpose     
 :------- | :------------    | :------------ 
 SCB (EZI2C) (PDL) | CYBSP_EZI2C          | EZI2C slave driver to communicate with CAPSENSE&trade; Tuner
 CAPSENSE&trade; | CYBSP_MSC | CAPSENSE&trade; driver to interact with the MSCLP hardware and interface the CAPSENSE&trade; sensors 
 Digital pin     | CYBSP_USER_LED1, CYBSP_USER_LED2 | To show the touchpad operation
 PWM | CYBSP_PWM | To drive the user LED which visualizes touchpad response


<br>

### Firmware flow

**Figure 28. Firmware flowchart**

<img src="images/firmware_flow.png" alt="Figure 28" width="400"/>



## Related resources

Resources  | Links
-----------|----------------------------------
Application notes  | [AN79953](https://www.infineon.com/AN79953) – Getting started with PSOC&trade; 4 <br> [AN85951](https://www.infineon.com/AN85951) – PSOC&trade; 4 and PSOC&trade; 6 MCU CAPSENSE&trade; design guide <br> [AN234231](https://www.infineon.com/AN234231) – PSoC&trade; 4 CAPSENSE&trade; ultra-low-power capacitive sensing techniques
Code examples | [Using ModusToolbox&trade;](https://github.com/Infineon/Code-Examples-for-ModusToolbox-Software) on GitHub
Device documentation | [PSOC&trade; 4 datasheets](https://www.infineon.com/cms/en/search.html#!term=psoc%204%20datasheet&view=all) <br>[PSOC&trade; 4 technical reference manuals](https://www.infineon.com/cms/en/search.html#!term=psoc%204%20TRM&view=all)
Development kits | Select your kits from the [Evaluation board finder](https://www.infineon.com/cms/en/design-support/finder-selection-tools/product-finder/evaluation-board).
Libraries on GitHub  | [mtb-pdl-cat2](https://github.com/Infineon/mtb-pdl-cat2) – PSOC&trade; 4 Peripheral Driver Library (PDL) 
Middleware on GitHub | [capsense](https://github.com/Infineon/capsense) – CAPSENSE&trade; library and documents
Tools  | [ModusToolbox&trade;](https://www.infineon.com/modustoolbox) – ModusToolbox&trade; software is a collection of easy-to-use libraries and tools enabling rapid development with Infineon MCUs for applications ranging from wireless and cloud-connected systems, edge AI/ML, embedded sense and control, to wired USB connectivity using PSOC&trade; Industrial/IoT MCUs, AIROC&trade; Wi-Fi and Bluetooth&reg; connectivity devices, XMC&trade; Industrial MCUs, and EZ-USB&trade;/EZ-PD&trade; wired connectivity controllers. ModusToolbox&trade; incorporates a comprehensive set of BSPs, HAL, libraries, configuration tools, and provides support for industry-standard IDEs to fast-track your embedded application development.

<br>



## Other resources


Infineon provides a wealth of data at [www.infineon.com](https://www.infineon.com) to help you select the right device, and quickly and effectively integrate it into your design.



## Document history

Document title: *CE240556* - *PSOC&trade; 4: MSCLP low power self-capacitance touchpad with 4mm overlay*

 Version | Description of change
 ------- | ---------------------
 1.0.0   | New code example 
 2.0.0   | Major update to support ModusToolbox&trade; v3.3. This version is not backward compatible with previous versions of ModusToolbox&trade;
 3.0.0   | Major update to support ModusToolbox&trade; v3.5. This version is not backward compatible with previous versions of ModusToolbox&trade;
<br>



All referenced product or service names and trademarks are the property of their respective owners.

The Bluetooth&reg; word mark and logos are registered trademarks owned by Bluetooth SIG, Inc., and any use of such marks by Infineon is under license.


---------------------------------------------------------

© Cypress Semiconductor Corporation, 2022-2024. This document is the property of Cypress Semiconductor Corporation, an Infineon Technologies company, and its affiliates ("Cypress").  This document, including any software or firmware included or referenced in this document ("Software"), is owned by Cypress under the intellectual property laws and treaties of the United States and other countries worldwide.  Cypress reserves all rights under such laws and treaties and does not, except as specifically stated in this paragraph, grant any license under its patents, copyrights, trademarks, or other intellectual property rights.  If the Software is not accompanied by a license agreement and you do not otherwise have a written agreement with Cypress governing the use of the Software, then Cypress hereby grants you a personal, non-exclusive, nontransferable license (without the right to sublicense) (1) under its copyright rights in the Software (a) for Software provided in source code form, to modify and reproduce the Software solely for use with Cypress hardware products, only internally within your organization, and (b) to distribute the Software in binary code form externally to end users (either directly or indirectly through resellers and distributors), solely for use on Cypress hardware product units, and (2) under those claims of Cypress's patents that are infringed by the Software (as provided by Cypress, unmodified) to make, use, distribute, and import the Software solely for use with Cypress hardware products.  Any other use, reproduction, modification, translation, or compilation of the Software is prohibited.
<br>
TO THE EXTENT PERMITTED BY APPLICABLE LAW, CYPRESS MAKES NO WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, WITH REGARD TO THIS DOCUMENT OR ANY SOFTWARE OR ACCOMPANYING HARDWARE, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  No computing device can be absolutely secure.  Therefore, despite security measures implemented in Cypress hardware or software products, Cypress shall have no liability arising out of any security breach, such as unauthorized access to or use of a Cypress product. CYPRESS DOES NOT REPRESENT, WARRANT, OR GUARANTEE THAT CYPRESS PRODUCTS, OR SYSTEMS CREATED USING CYPRESS PRODUCTS, WILL BE FREE FROM CORRUPTION, ATTACK, VIRUSES, INTERFERENCE, HACKING, DATA LOSS OR THEFT, OR OTHER SECURITY INTRUSION (collectively, "Security Breach").  Cypress disclaims any liability relating to any Security Breach, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any Security Breach.  In addition, the products described in these materials may contain design defects or errors known as errata which may cause the product to deviate from published specifications. To the extent permitted by applicable law, Cypress reserves the right to make changes to this document without further notice. Cypress does not assume any liability arising out of the application or use of any product or circuit described in this document. Any information provided in this document, including any sample design information or programming code, is provided only for reference purposes.  It is the responsibility of the user of this document to properly design, program, and test the functionality and safety of any application made of this information and any resulting product.  "High-Risk Device" means any device or system whose failure could cause personal injury, death, or property damage.  Examples of High-Risk Devices are weapons, nuclear installations, surgical implants, and other medical devices.  "Critical Component" means any component of a High-Risk Device whose failure to perform can be reasonably expected to cause, directly or indirectly, the failure of the High-Risk Device, or to affect its safety or effectiveness.  Cypress is not liable, in whole or in part, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any use of a Cypress product as a Critical Component in a High-Risk Device. You shall indemnify and hold Cypress, including its affiliates, and its directors, officers, employees, agents, distributors, and assigns harmless from and against all claims, costs, damages, and expenses, arising out of any claim, including claims for product liability, personal injury or death, or property damage arising from any use of a Cypress product as a Critical Component in a High-Risk Device. Cypress products are not intended or authorized for use as a Critical Component in any High-Risk Device except to the limited extent that (i) Cypress's published data sheet for the product explicitly states Cypress has qualified the product for use in a specific High-Risk Device, or (ii) Cypress has given you advance written authorization to use the product as a Critical Component in the specific High-Risk Device and you have signed a separate indemnification agreement.
<br>
Cypress, the Cypress logo, and combinations thereof, ModusToolbox, PSoC, CAPSENSE, EZ-USB, F-RAM, and TRAVEO are trademarks or registered trademarks of Cypress or a subsidiary of Cypress in the United States or in other countries. For a more complete list of Cypress trademarks, visit www.infineon.com. Other names and brands may be claimed as property of their respective owners.
