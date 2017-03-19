# Vim

> To a text editor, I'm always concerning about these factors:
0. simplicity of the high-frequent operation:
   + insert a char
   + select a block
   + copy and paste
   + move cursor to a desired place
1. compatibility with Unicode

When we say 'word', it representing the string made up of characters, numbers, and '_'.
And 'blank' includes space, tab, '\n\r'

### Basic commands
key|command
:---:|:---:
i|insert mode
x|delete one char
:wq|save and exit
dd|delete this line
p|paste after cursor
P|paste before cursor
hjkl| move to up/down/left/right

### Normal mode

Insert mode:

key|command
:---:|:---:
a|insert after cursor
o|add a line before cursor
O|same as 'o'
cw|move cursor to end of a word

Move cursor:

key|command
:---:|:---:
0|to head of line
^|first char that's not blank
$|to end of line
g_|last char that's not blank

Other:

key|command
:---:|:---:
/word|search words matching 'word' (press 'n' to next)
yy|copy this line
u|undo
ctrl-r|redo
ZZ|save if needed and exit

Useful shortcuts:

key|command
:---:|:---:
.|repeat last command
N< command >|repeat < command > N times
N G|to Nth line
:N|to Nth line (command mode)
gg|to first line
G|to last line
w|to head of next word
e|to end of previous word

### Command mode
Press ':' in normal mode into command mode.

key|command
:---:|:---:
e < dir >|open file in < dir >
w|save
saveas < dir >|save as < dir >
x| save if needed and exit
wq|same as 'x'
q!|exit without save
qa!|force to exit without save
bn|to next file (when opening several files)
n|same with bn
bp|to previous file
