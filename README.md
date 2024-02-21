# PnR-eel
Punch and Roll script for Reaper DAW written in EEL

This script provides a single button custom action to find a break in the audio, play a lead in and then restart recording\
//99% of this is taken from JRK's solution for moving markers to quiet spaces found here https://forums.cockos.com/showthread.php?t=250487 \
// I just swapped out the iterated marker moving and swapped in moving the edit cursor (then restarting recording)\
// waiting code came from NoFish, who got it from Schwa here https://forum.cockos.com/showthread.php?t=168270 \

***** Requires the  SWS extension be installed. Download it here: https://www.sws-extension.org/

Variables for customization follow:

////////////////////////// User edits ///////////////////////////////////////\
SOURCE_TRACK = 0 ; // set the controlling track !!Zero Indexed!! meaning "0" = track 1\
BEATS_BACK = 4; // number of beats to move back before searching for silence\
PNR_MEASURES_PREROLL = 4; // set the number of measures to play before recording\
TIME_UNTIL_REMUTE = 5; //how long to wait until re-muting the track (if it was muted before)\
 <code>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;</code>//I'd advise keeping this slightly longer than your play in (PNR_MEASURES_PREROLL)\
 <code>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;</code>//because the countdown starts at the beginning of the play in\

//setting BPM to sixty with time signature of 1/4 means each beat is 1 second and each measure is 4 seconds\
PNR_BPM = 60; // bpm to use while moving edit cursor\
PNR_TIMESIG_NUMERATOR = 1; //sets numerator of time signature during PnR operation\
PNR_TIMESIG_DENOMINATOR = 4; //set denominator of time signture during PnR operation\

//technical stuff\
THRESHOLD = 0.006;  // sound level below which a block is considered "silent"\
WINDOW_TIME = 0.25; // size of block to check for exceeding threshold\
SEARCH_INCREMENT = .01; //offset to incrementally shift the block left when searching for silent gap end and beginning\
SLICE_OFFSET = .3; // percent to move cursor forward into silent area after determing beginning of silent section\
 <code>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;</code>// to avoid clipping off the end of a word\
/////////////////////////////////////////////////////////////////////////////\
