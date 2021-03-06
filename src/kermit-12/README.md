# KERMIT-12: Kermit Software for the Digital Equipment Corporation PDP-8 and PDP-12

Written by Jerry Sands, Randy Hippe, Martyn Hemmings, Sepp Stadelmann, Richard Schlerf, and Charles Lasner.

The codeline here uses [Columbia Kermit-12 Archive Distribution k12.tar.gz][k12-dist] as upstream.
Another source is [ibiblio.org k12][ibiblio].  The Columbia Archive has two differences: text files k12mit.not,
and k12mit.dsk are more up-to-date.

[kermitproject.org][org-project] says:

Kermit is a robust transport-independent file-transfer protocol and a large collection of software programs
that implement it on a [wide variety of platforms][platforms]. In addition to file transfer, many of these programs also
make network, dialed, and/or serial-port connections and also offer features such as terminal emulation,
character-set conversion, and scripting for automation of any communication or file-management task.
The Kermit Project originated at Columbia University in New York City in 1981 and remained there for 30 years.
Since 2011 it is independent. [CLICK HERE][project] for more about the Kermit Project.

The [Kermit-12 Site at Columbia][columbia-k12] was frozen in 2011, but still has useful information
(even though many links there no longer work.) Excerpts from that page:

Kermit-12 was written for DEC 12-bit processors including PDP-8, the PDP-12 laboratory computer,
and the DECmate I, II, and III, WT-78, VT-78, and VT-278 word processors.

It runs under OS/8, OS/78, OS/278, and OS/12.

File types found in the Kermit-12 distribution are:

| File type | Description
| --------- | -------------------------------------------------
| .ann	    | Announcements (plain ASCII text).
| .boo	    | ASCII-encoded binary encoding to be decoded by k12deb.sv
| .bwr	    | "Beware" file (hints and tips).
| .doc	    | Plain-text ASCII documentation.
| .dsk	    | Description of files (plain text).
| .enc	    | ASCII-encoded 12-bit binary encoding to be decoded by k12dec.sv
| .ipl	    | Initial program ("bootstrap") loader.
| .lst	    | Load map.
| .not	    | Notes.
| .odt	    | Octal Debugging Technique (bootstrapping).
| .pal	    | PAL-8 assembly language source code.
| .upd	    | Update notes.

## Operating Instructions

(Extracted from k12mit.pal)

KERMIT-12 FOR THE FAMILY OF 12-BIT DEC MACHINES.

**BRIEF USAGE DESCRIPTION.**

KERMIT-12 IS AN IMPLEMENTATION OF THE KERMIT PROTOCOL FOR THE FAMILY OF 12-BIT
DEC (AND COMPATIBLE) MACHINES GENERALLY KNOWN AS PDP-8 OR DECMATE.

AS OF THE CURRENT IMPLEMENTATION, THE FOLLOWING COMMANDS ARE EFFECTIVE:

1.	CONNECT (TO REMOTE SYSTEM AS TERMINAL).

2.	SEND FILESPEC (TO REMOTE RECEIVER OR SERVER).

3.	RECEIVE FILESPEC (FROM REMOTE SENDER).

4.	GET FILESPEC (FROM REMOTE SERVER).

5.	FINISH (SERVING).

6.	SETUP (ON DECMATE II/III/III-PLUS ONLY). **** NOT IMPLEMENTED ****

7.	EXIT (TO OPERATING SYSTEM).

8.	HELP (DISPLAYS HELP MESSAGE).

FILESPEC  MAY  BE  ANY LOCAL (OS/8) FILE-STRUCTURED DEVICE:FILENAME.EXTENSION,
WHERE THE  FILENAME  AND  EXTENSION WILL BE TRUNCATED TO 6 ALPHANUMERICS AND 2
ALPHANUMERICS RESPECTIVELY, AS  NECESSARY (THIS IS REFERRED TO AS 6.2 FILENAME
FORMAT).  THE DEVICE:    FIELD  IS  OPTIONAL;   ALL COMMANDS USING THE DEVICE:
FIELD FOR LOCAL DEVICE SPECIFICATION  WILL  USE  THIS  DEVICE AS THE SOURCE OR
DESTINATION AS NECESSARY FOR THE LOCAL  FILES.    IF  THE  DEVICE:    FIELD IS
OMITTED, THE DEFAULT DEVICE DSK:  WILL BE USED.  THE ACTUAL DEVICE USED MAY BE
SELECTED BEFORE INVOKING KERMIT-12 BY USING THE OS/8 ASSIGN COMMAND:

.ASSIGN DEV DSK

WHERE DEV IS ANY AVAILABLE FILE-STRUCTURED DEVICE.

KERMIT-12 USES AN UNUSUAL SCHEME FOR ITS PROMPT:    THE  ACTUAL DEFAULT PROMPT
TEXT  IS  PARTIALLY  TAKEN  FROM  THE  ACTUAL MACHINE KERMIT-12  IS  CURRENTLY
EXECUTING  ON.    FOR  EXAMPLE, IF KERMIT-12 HAS DETERMINED THE  CPU  TYPE  AS
PDP-8/E, THE PROMPT WILL BE:

KERMIT-8/E>

THIS  ALLOWS KERMIT-12 USERS (WITH DIFFERENT CPU-TYPE MACHINES) TO DISTINGUISH
MESSAGES ORIGINATING  FROM  THE  RESPECTIVE  SYSTEMS.    FUTURE  VERSIONS WILL
SUPPORT USER PROMPT STRINGS TO ALLOW MORE DISTINCTIVE SYSTEM MESSAGES.

THE HELP OR CONNECT COMMANDS MAY BE USED TO DETERMINE THE CURRENT CONNECT MODE
ESCAPE CHARACTER.

**COMMAND RESTRICTIONS**

THE  SEND  COMMAND  ALLOWS   DEVICE:FILENAME.EXTENSION  (6.2)  WITH  WILD-CARD
SUBSTITUTION.  A * MAY  BE  GIVEN  FOR  AN  ENTIRE  FIELD  (EITHER FILENAME OR
EXTENSION OR BOTH) ONLY.  A  ?    WILL  MATCH  ANY SINGLE CHARACTER WHICH MUST
EXIST IN THE ACTUAL FILENAME OR EXTENSION,  UNLESS  RIGHT-MOST  IN  THE FIELD.
ALL  MATCHING FILES WILL BE SENT.  NO  OUTBOUND  FILENAME  (AS-NAME)  FACILITY
EXISTS AT THIS TIME.

THE  RECEIVE  COMMAND  ALLOWS  OPTIONAL  DEVICE:   ONLY.   *THE  FILENAME  AND
EXTENSION  ARE  NOT  ALLOWED*.  NAMES OF RECEIVED FILES WILL  BE  MODIFIED  IF
NECESSARY  TO  CONFORM  TO  THE  6.2  FORMAT.   *IMPLEMENTATION RESTRICTION* :
CERTAIN REMOTE  FILENAMES  CONTAINING  NON-ALPHANUMERIC  CHARACTERS  MAY CAUSE
KERMIT-12 TO HASTILY ABORT THE TRANSMISSION AND RETURN TO COMMAND LEVEL.

THE GET COMMAND  ALLOWS  OPTIONAL  DEVICE:    TO  DETERMINE DESTINATION OF THE
INCOMING FILES.  THE  OUTBOUND  FILESPEC  MUST  CONFORM  TO  LOCAL CONVENTIONS
(FILENAME AND EXTENSION ARE NOT  LIMITED  TO  6.2  FORMAT;  THE DEVICE:  FIELD
WILL NOT BE SENT TO THE  REMOTE  KERMIT  UNLESS  IT  IS  ILLEGAL  WITHIN  OS/8
SPECIFICATIONS, SUCH AS TOO MANY DEVICE LETTERS.    IN  THIS CASE, THE DEFAULT
DEVICE DSK:  APPLIES, AND THE ENTIRE "DEVICE"  FIELD  IS  SENT  ALONG WITH ANY
FILENAME  AND EXTENSION).  CERTAIN REMOTE SYSTEMS ARE INCOMPATIBLE  WITH  THIS
IMPLEMENTATION,  AS  IMBEDDED  SPACES  OR  NON-ALPHANUMERIC CHARACTERS ARE NOT
ALLOWED, EVEN  THOUGH  THEY  MAY  BE REQUIRED ON THE REMOTE SYSTEM.  WILD-CARD
CHARACTERS ARE ALLOWED, BUT ONLY AS SPECIFIED IN THE SEND COMMAND ABOVE.

<^X>  OR  <^Z>  CAN BE USED TO ABORT KERMIT TRANSMISSIONS (EVENTUALLY) BUT  IS
NORMALLY  A  SLOW  PROCESS,  SINCE  THE CHECKING IS DONE BY A SOFTWARE TIMEOUT
SCHEME.   AT  THE  PRESENT  TIME,  THERE  IS  NO DISTINCTION BETWEEN THESE THO
CHARACTERS, SO IT  IS NOT POSSIBLE TO ABORT A SINGLE FILE; THE ENTIRE BATCH OF
FILES INVOLVED IN THE TRANSFER IS ABORTED.

**DECMATE II/III/III-PLUS CONSIDERATIONS**

FUNCTION KEYS SEND <ESC>  SEQUENCES SPECIFIED BY SLUSHWARE/FIRMWARE.  ALL SOFT
FUNCTION KEYS ARE THEREFORE INEFFECTIVE  (EXCEPT  FOR HOLD SCREEN WHICH ALWAYS
WORKS).

CONNECT MODE RUNS IN 8-BIT MODE.

THE COMPOSE KEY IS ENABLED FOR USE WITH A LOADED COMPOSE TABLE.

ANY VALID DECMATE II/III/III-PLUS CHARACTER SET  IS  ALLOWED  WHILE IN CONNECT
MODE  (MCS  TCS  LINE,  ETC.).    ALL   <ESC>  SEQUENCES  ARE  PASSED  TO  THE
SLUSHWARE/FIRMWARE UNMODIFIED.

KEYBOARD UPPER-CASE LOCK WILL ALWAYS BE AUTOMATICALLY APPLIED UPON RETURN FROM
CONNECT MODE.


[platforms]: http://www.kermitproject.org/archive.html
[project]: http://www.kermitproject.org/kermit.html
[columbia-k12]: http://www.columbia.edu/kermit/pdp8.html
[org-project]: http://www.kermitproject.org/
[k12-dist]: http://www.columbia.edu/kermit/ftp/archives/k12.tar.gz
[ibiblio]: http://www.ibiblio.org/pub/academic/computer-science/history/pdp-8/kermit/k12/