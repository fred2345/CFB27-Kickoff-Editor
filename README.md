# CFB27-Kickoff-Editor
This tool allows you to edit your kickoff times and WILL have the correct lighting for whatever time you chose
============================================================
CFB 27 GAME TIME EDITOR v1.0
COMPLETE SETUP + USAGE INSTRUCTIONS
============================================================

WHAT THIS IS
-------------
CFB 27 Game Time Editor v1.0 is a Windows desktop utility for changing
kickoff times in a College Football 27 Dynasty save.

v1.0 is the PROVEN kickoff-editing baseline. It uses the minimal-diff
writer that has been tested successfully on a real/main CFB 27 Dynasty
save.

IMPORTANT:
- This tool edits the selected Dynasty save in place after validation.
- ALWAYS work from a BACKUP COPY of your Dynasty save.
- Never use your only copy of a Dynasty save as the selected file.
- v1.0 only changes kickoff TimeOfDay data. Do not expect it to edit other
  Dynasty settings.

============================================================
1. WHAT YOU NEED
============================================================

OPERATING SYSTEM
----------------
Windows 10 or Windows 11 is recommended.

REQUIRED SOFTWARE
-----------------
1. Node.js + npm
2. Python 3
3. Internet access the first time you run the tool, so npm can install
   the required madden-franchise package and Python can install deflate
   if needed.

Node.js includes npm. Use a supported Node.js LTS release. The official
Node.js download page is:
https://nodejs.org/en/download/

Python:
https://www.python.org/downloads/

During Node.js installation, use the normal Windows installer defaults
and make sure Node.js/npm are added to PATH.

During Python installation, enable:
[✓] Add Python to PATH

============================================================
2. INSTALL / PREPARE THE TOOL
============================================================

STEP 1 - EXTRACT THE ZIP
------------------------
Right-click the v1.0 ZIP and choose:

Extract All...

Extract it somewhere easy to find, for example:

C:\CFB27\GameTimeEditor\

After extraction you should see a folder similar to:

CFB27_Game_Time_Editor_v1_0

Inside it are:
- editor.mjs
- start.bat
- package.json
- libdeflate-compress.py
- README.txt

DO NOT run editor.mjs directly by double-clicking it.
Use start.bat.

STEP 2 - VERIFY NODE.JS
-----------------------
Open Command Prompt and run:

node -v
npm -v

Both commands should print a version number.

STEP 3 - VERIFY PYTHON
----------------------
Run:

py -3 --version

or:

python --version

At least one of those should print a Python 3 version.

============================================================
3. FIRST RUN
============================================================

STEP 1
------
Double-click:

start.bat

STEP 2
------
A Windows file-selection window will appear.

Select your BACKUP CFB 27 Dynasty save.

The save can have a normal Dynasty filename or the game's autosave-style
filename. The editor does not require a .sav extension.

STEP 3
------
On the first run, the tool may automatically do the following:

- install the npm dependency madden-franchise
- install the Python deflate package if it is missing

Allow those installations to finish.

STEP 4
------
The editor will read the Dynasty and display the games it can edit.
Follow the on-screen prompts to select the game and enter the desired
kickoff time.

============================================================
4. CHANGING A KICKOFF TIME
============================================================

1. Start start.bat.
2. Select your BACKUP Dynasty save.
3. Find the game you want to edit.
4. Select the game.
5. Enter the desired kickoff time.
6. Let the editor complete its validation.
7. Do not close the Command Prompt while the save is being processed.
8. When the tool reports success, close it.
9. Copy/use the edited backup in CFB 27.

Example:

Original:
NIU @ Iowa - 12:00 PM

Target:
NIU @ Iowa - 7:30 PM

The editor converts the selected time to the game's TimeOfDay value,
performs the minimal-diff write, reopens the result, and validates the
changed value before finishing.

============================================================
5. HOW THE SAFE WRITER WORKS
============================================================

v1.0 is intentionally conservative.

The writer:

1. Parses the Dynasty using the known-good CFB 27 parser configuration.
2. Identifies the selected SeasonGame record.
3. Changes only TimeOfDay in a comparison buffer.
4. Compares the edited database buffer against the original database.
5. Detects the exact byte ranges caused by the kickoff-time change.
6. Applies only those detected byte changes to the ORIGINAL database.
7. Recompresses the database with the required compression path.
8. Preserves the original FBCHUNKS container/tail data.
9. Reopens the generated save.
10. Confirms the selected game's TimeOfDay is the requested value.
11. Only then completes the overwrite operation.

SAFETY LIMITS
-------------
The tool intentionally aborts if the supposed one-field edit causes:

- more than 64 changed database bytes, OR
- more than 16 changed byte ranges.

If that happens, the tool stops rather than risking unrelated Dynasty data.

DO NOT REMOVE THESE SAFETY LIMITS.

============================================================
6. BACKUP RULES
============================================================

BEFORE EVERY EDIT:

1. Make a copy of the Dynasty save.
2. Give the copy a clear name, for example:

DYNASTY-BEFORE-KICKOFF-EDIT

3. Use that copy with v1.0.
4. Keep the original untouched until you have loaded the edited save in
   CFB 27 and confirmed everything works.

For especially important Dynasties, keep multiple dated backups.

============================================================
7. WHAT v1.0 DOES NOT DO
============================================================

v1.0 is intentionally limited to kickoff-time editing.

It does NOT currently provide a general Dynasty editor for:

- teams
- players
- ratings
- conferences
- rankings
- schedules beyond kickoff TimeOfDay
- recruiting
- coaches
- uniforms
- stadiums
- playoff settings
- other Dynasty database fields

Those can be considered for future versions only after the v1.0 baseline
remains preserved.

============================================================
8. TROUBLESHOOTING
============================================================

ERROR: 'node' is not recognized
--------------------------------
Node.js is not installed or is not on PATH.

Install Node.js from the official Node.js website, restart Command Prompt,
and run:

node -v
npm -v

again.

ERROR: 'npm' is not recognized
------------------------------
Reinstall Node.js using the Windows installer and make sure npm is added
to PATH. Restart Windows/Command Prompt afterward if necessary.

ERROR: Python / deflate package missing
---------------------------------------
Run:

py -3 -m pip install deflate

Then run start.bat again.

If 'py' is unavailable, try:

python -m pip install deflate

ERROR: npm install failed
-------------------------
Confirm you have internet access and run start.bat again.

If necessary, open Command Prompt inside the tool folder and run:

npm install

Do not delete package.json.

ERROR: Save cannot be parsed
----------------------------
Make sure the selected file is an actual CFB 27 Dynasty save and not a
cloud placeholder, screenshot, compressed archive, or unrelated file.

Try another backup of the same Dynasty.

ERROR: Safety abort / too many byte changes
--------------------------------------------
STOP.

Do not force the save through the editor.
The safety system is doing its job. A kickoff-only change should remain a
small/minimal database modification.

Keep the original backup untouched and report the exact console output.

CFB 27 hangs or refuses to load the edited save
------------------------------------------------
v1.0 has been successfully tested on a main Dynasty save, but always keep
a clean backup.

If a particular edit causes a loading problem:

1. Do not overwrite your clean original.
2. Re-run the editor from a fresh backup.
3. Try the same game/time once more.
4. Save the complete console output if it fails.

============================================================
9. RECOMMENDED FOLDER SETUP
============================================================

A simple setup is:

C:\CFB27\
  GameTimeEditor\
    CFB27_Game_Time_Editor_v1_0\
  DynastyBackups\
    MyDynasty-CLEAN
    MyDynasty-BEFORE-EDIT
    MyDynasty-EDITED

Keep the tool folder separate from your game's save folders.

============================================================
10. VERSION BASELINE
============================================================

CURRENT VERSION: v1.0

v1.0 = proven kickoff-time editing baseline.

The v1.0 writer should be treated as the known-good foundation.
Future versions should preserve the proven v1.0 behavior unless a change
is deliberately being tested and documented.

============================================================
11. QUICK START
============================================================

For experienced users:

1. Install Node.js + npm.
2. Install Python 3.
3. Extract the v1.0 ZIP.
4. Double-click start.bat.
5. Select a BACKUP Dynasty save.
6. Select the game.
7. Enter the new kickoff time.
8. Wait for validation to finish.
9. Test the edited save in CFB 27.
