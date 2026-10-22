<img src="img/UNF_Logo.png" alt="UNF logo" width="350"/>

UNF 3T generic procedures

#### Authors:
Daniel Papp<br>
MRI Physicist<br>
2023

André Cyr<br>
Biomedical engineer<br>
2026

Version|Initials|Date|Comment
-|-|-|-
1|DP|2023-mm-dd|[VE11C version](https://docs.google.com/document/d/1HEWXVibZwXJ7bnu6kPV44Odulyyic9UGxWoa1FFlNLs/edit?usp=drive_link)
2|AC|2026-10-19|XA60A version

[Emergency contact information](https://docs.google.com/document/d/1DNDpuEd6Fl_4Pvpz14diZwGYx1c003gBqGrLvVqvCYg/edit?usp=drive_link)<br>

# Table of contents

1. Console management
    1. [Register a new patient](#regpat)
    1. [Saving a scan session as a new protocol](#save_session_as_protocol)
    1. [Disabling kiosk mode (formerly Enable advanced user mode on VE11)](#adv-user)
    1. [Expert-i access](#experti)
    1. [Installing sequences and security certificates](#seq_install)
1. Running scans
    1. [FOV positioning](#fov)
    1. [Table positioning mode](#tablepos)
    2. [Reversing the Phase Encoding Direction](#pe_rev)
    1. [Multiplanar reconstruction](#mpr)
    1. [Advanced shimming](#advshim)
    1. [Enabling or disabling distortion correction](#dist-corr)
    1. [Using coupled graphics](#coupled-graphics)
    1. [PMU recording](#pmu-recording)
1. Post scannning
    1. [Adding image comments](#image-comment)
    1. [Correct data before transferring](#pt_correct)
    1. Transfer data to server
    1. Transfer raw image data
1. [Troubleshooting](#troublesooting)
    1. [What to do if the scanner hangs](#scanner-hang)


# List of acronyms
AC-PC : Anterior Commissure - Posterior Commissure<br>
EPI : EchoPlanar Imaging<br>
FOV : Field of view<br>
MPR : Multiplanar Reconstruction<br>
PMU : Patient Monitoring Unit<br>
VOI : Volume of interest<br>

# Console management

## <a name="regpat">Register a new patient</a>
1. Press the register new patient key (0 on the numeric keypad), or click on the register new patient icon .

<img src="img/regpat_key.png" alt="" width="300"/>
 or
<img src="img/regpat_icon.png" alt="" width="300"/>

2. Enter the session name in the field `Last Name`. The session name should match what was entered on the MRI calendar when booking the session. **Important: Never enter the participant's actual name** If a participant's name is mistakenly entered on the console, data should be corrected before being transfered to server. Correction procedure [here](#pt_correct)

3. Press the `Tab` key a few times to advance through the fields. When focus is on `Patient ID`, press `Tab` once more to automatically generate a unique patient ID.

4. Fill in the next mandatory fields Date of birth, Sex, Height and Weight.

5. In the field `Referring physician`, enter the appropriate gid for the session. The config file is located  [here](https://github.com/UNFmontreal/bids_configs/blob/master/studies.json).

6. Enter operator's initials in field `Operator`

7. Select the appropriate program from the `program selection` dialog and appropriate patient orientation (usually Head First Supine)

8. Click `Save` to store that patient for future scanning or `Exam` to start scanning with that patient.

## <a name="save_session_as_protocol">Saving a scan session as a new protocol</a>

  ### If the session is still opened in the exam card
  1. Right-click in the sequence listing area and select `Save as`<br>
  <img src="img/save_session_as_protocol_1.png" alt="" width="250"/>
  1. Browse the trees for the location you want to save your new program and enter the name you want to give it<br>
  <img src="img/save_session_as_protocol_2.png" alt="" width="250"/>


  ### If the session is closed
  1. Open `myExamCockpit` and navigate to the tree where you want to create the new protocol
  1. Right-click in the tree and select `New`, then `Program`
  1. Click `Save program as` and enter the name you want to give it
  1. Open the patient browser by clicking on the  icon at the top left in the examination workflow<br>
  <img src="img/patient_browser.png" alt="" width="250"/>
  1. Select the scanning session you want to save in the `Results` pane on the left
  1. In the `Series` pane on the right, click the PhoenixZIPReport series and drag it in your opened program. A + signs will appear next to the cursor<br>
  <img src="img/phoenix_report_1.png" alt="" width="350"/>
  1. Close the program and save the changes


  ## <a name="adv-user">Disabling kiosk mode (formerly Enable advanced user mode on VE11)</a>

  ### Description:
  Advanced User mode allows the Scanner Operator to access more features than in normal operating mode, such as mounting external drives, copying data, installing new sequences and ICE programs, etc. Please note that all procedures detailed after this one require “Advanced User” mode to be enabled

  ### Procedure:
  Hit `TAB` + `DEL` + `NUMPAD + or Send to PACS` on the keyboard to open a login menu. Enter `medadmin` as the user name and type in the password.

  <img src="img/disable_kiosk_mode.png" alt="UNF logo" width="500"/><br>


## <a name="experti">Expert-i access</a>
Expert-i allows a remote user to connect to connect and interact with the SYNGO console. It can be useful for remote troubleshooting or for collaboration.

**The remote user needs a connection to the CRIUGM VPN**

The remote user can use Fortigate client (FortiClient) or OpenFortiVPN CLI. They need to set up a connection to **206.167.239.2** on port **443** and use their credentials provided by the IT from CRIUGM to establish the connection. It is recommended to set up and test this part prior to attempting an Expert-i connection, i.e. not in the middle of a scanning session.

<img src="img/VPN.png" alt="" width="400"/><br>
VPN connection parameters


### To start an Expert-i session

#### On the SYNGO Console
1. Click on the expert-i icon <img src="img/expert-i_icon.png" alt="" width="25"/> in the top right corner of the screen
2. Select `Provide Expert-i access`<br>
<img src="img/provide_expert-i_access.png" alt="" width="125"/><br>
3. Choose the connection mode. View only will allow the remote user to see the whole content of the screen, but not to interact with it while Full Access will allow the remote user to control the scanner in the same way as if they were at the console
4. Click on `Allow Connection`
5. Give the 4 digits access code to the remote user who will then have 2 minutes to connect before the session times out.

#### On the remote computer
After the connection to CRIUGM VPN is established, the remote user can launch Siemens Expert-i application on their Windows computer, or they can direct an internet browser to https://10.30.16.5:7443/syngo.experti. If using the browser method, the user will have to accept the certificate security warning and click on "Proceed to site anyway".

After the connection is established, the remote user will see the whole Syngo screen. If the connection mode is View only, they will not be able to interact with the console, but they will be able to move a cursor to point elements to the console operator. If the connection mode is Full Access, they will be able to interact fully with the console as if they were sitting in front of it.



## <a name="seq_install">Installing sequences and security certificates</a>

### Install Security Certificate

#### 1. Deactivate kiosk mode
If not done already, [deactivate kiosk mode](#adv-user)

#### 2. Check if certificate needs to be installed

##### Case 1: An installer is provided for the sequence
1. Copy the installer on the console e.g. in `C:\temp`
1. Double-click on installer (.exe file) **Do not** try to run it as an administrator yet. This step will fail, but the error message will tell you whether the certificates are installed or not.

If this error message appears:<br>
<img src="img/no_cert.png" alt="" width="400"/><br>
then the certificates are not installed. Proceed to next step to install them.

If this error message appears:<br>
<img src="img/cert_ok.png" alt="" width="400"/><br>
then the certificates are installed and you can proceed to installation by right-clicking the executable file and select `Run as administrator`


##### Case 2: No installer is provided

  1. Copy sequence files in:<br>
  `C:\ProgramData\Siemens\Numaris\MriCustomer\CustomerSeq`

  1. Copy reconstruction files in:<br>
  `C:\ProgramData\Siemens\Numaris\MriCustomer\Ice`

  1. Try to load the sequence from the DEFAULT tree - Customer Sequences region

#### 3. Install certificate
  1. Copy certificate (.cer) file on disk
  1. Right-click on file and choose `Install certificate`<br>
    <img src="img/cert_inst_01.png" alt="" width="300"/><br><br>
  1. Select `Local machine` as Store Location<br>
  <img src="img/cert_inst_02.png" alt="" width="300"/><br><br>
  1. Enter admin Credentials
  1. Select `Place all certificates in the following store`, then click browse
  1. Select `Trusted Root Certification Authorities` and click `OK`<br>
  <img src="img/cert_inst_03.png" alt="" width="300"/><br><br>
  1. Click `Next`
  1. Click `Finish`<br>
  <img src="img/cert_inst_04.png" alt="" width="300"/><br><br>

#### 4. Register certificates with device guard
  1. Open admin command prompt or right-click normal command prompt, then select `run as administrator`<br>
  <img src="img/cmd_prompt.png" alt="" width="300"/><br><br>
  1. Type in admin credentials
  1. Type in `powershell`
  1. Type in `Set-ExecutionPolicy Bypass`
  1. Type in `Get-ExecutionPolicy` (check that status is actually set to bypass)
  1. Type in `& $env:MED_BIN\Scripts\DeviceGuardPreparation.ps1 C:\TEMP\MyCertificateName.cer` with the path to the certificate you installed on preceding step **Important** This step may appear to hang, but can take as long as 10 minutes to complete. Do not reboot system or close window.
  1. Repeat step 6 for each certificate you need to install
  1. Restart system. Full reboot is required - not just restart workplace

# Post scanning

## <a name="image-comment">Adding Image Comments</a>

### Description and use case:

## <a name="pt_correct">Correct data before transferring</a>
1. Open patient browser
<br><br><img src="img/patient_browser.png" alt="UNF logo" width="250"/><br><br>
1. Right-click on the patient to correct in the `Results` pane on the left
1. Select `Correct` option
1. Edit the information that you need to correct. Usually, it will be the Last name (session name) field in the patient tab or the Referring physician (gid) in the study tab
1. Click `OK` and accept the changes



# <a name="troubleshooting">Troubleshooting</a>
