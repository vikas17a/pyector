

See the Wiki for [the last version of this manual](http://code.google.com/p/pyector/source/browse/trunk/pyector/doc/txt/EctorManual.txt).

# Introduction #

Ector.py is the python module which contains the Ector class, but also the main program to use Ector.

This page explains how to use this program.


# Run it #

src/Ector.py is to be launched by typing this (provided that Python 2.5+ is installed on your system) in a shell, in the root directory of the pyector project:
```
python src/Ector.py
```

## Options ##
There are several options you can use.

Here is the synopsis of the command (version 0.2):
```
python Ector.py [-p username=User][-n botname=Ector][-l logfilepath=ector.log][-s|-g][-h]
```

### p --person ###
This option gives the user name to Ector.
It is the name under which you are recognized by Ector.
It will be used to create a file `username_state.pkl` in which it will save the last subjects you talk about (to simplify).

When you talk to Ector, you are named `username`, and nothing else. Don't use other pseudos or nicknames.
The username is displayed before the prompt, so that you always know what's your name ;)

By default, it is **`User`**.

You can always change this name during the interactive session by using the `@person` command:
```
User>@person Bill
Bill>
```

### n --name ###
You can change the name of the bot, but its default name will be **`Ector`**.
The name you give is capitalized.

### l --log ###
You can change the file in which the log is written.
By default, the file is `ector.log` and is saved in the current directory (from where you launch Ector).

This is the same as the `@log` command.

### h --help ###
The help option reminds the usage of the program:
```
$python src/Ector.py -h
Usage: Ector.py [-p username][-n botname=Ector][-v|-q][-l logfilepath=ector.log]
[-s|-g][-h]

Options:
  --version             show program's version number and exit
  -h, --help            show this help message and exit
  -p USERNAME, --person=USERNAME
                        set the name of the utterer
  -n BOTNAME, --name=BOTNAME
                        set the name of the bot
  -v                    say all that you can say
  -q                    shut up!
  -l LOGNAME, --log=LOGNAME
                        log the dialogue in log file
  -s, --sentence        set sentence reply mode on
  -g, --generate        set generate reply mode on
  -d, --debug           set debug mode on
```
Although some options are already present, they are not functional: -v, -q are not applicable, as Ector does not answer, even in version 0.2.


## Use it ##
Once you have launch the program, you get some license and copyright information:
```
$ python src/Ector.py
pyECTOR version 0.4, Copyright (C) 2008 Francois PARMENTIER
pyECTOR comes with ABSOLUTELY NO WARRANTY; for details type `@show w'.
This is free software, and you are welcome to redistribute it
under certain conditions; type `@show c' for details.
@help gives a basic help on pyECTOR commands.
User>
```

From there, you can either type sentences you want Ector to learn, or use some commands.
Let's see these commands.

### @help ###
Typing `@help`, then enter will display all available commands:
```
User>@help
You can just start typing phrases.
But there are some commands you can use:
 - @usage     : print the options of the Ector.py command
 - @quit      : quit
 - @exit      : quit
 - @bye       : quit
 - @person    : change the utterer name (like -p)
 - @name      : change the bot's name (like -n)
 - @version   : give the current version
 - @write     : save Ector's Concept Network and state
 - @shownodes : show the nodes of the Concept Network
 - @showlinks : show the links of the Concept Network
 - @log [file]: log the entries in the file (no file turns off the logging)
 - @status    : show the status of Ector (Concept Network, states)
 - @debug [ON|OFF]: set the debug mode on or off
User>
```

### @usage ###
Usage is the same than `-h, --help` option. It gives the synopsis of the program.

### @quit, @exit, @bye ###


`@quit`, `@exit`, and `@bye` are the same command: it is the only means to quit Ector.

**Warning**: at this point, if you did not save the ConceptNetwork (using `@write`), all you said since the last save will be lost!

### @person ###
The `@person` command let you change your name in the course of the interactive session:
```
User>@person Bill
Bill>
```

**Warning**: at this point, if you did not save, Ector won't remember your last conversation state the next time you return as `User`.

### @name ###
The `@name` command let you change the name of the bot, so that when you say this new name, the bot knows it is him.

**Tip**: don't use this command too much, except if you want to call the bot another name than "Ector".

### @version ###
Gives the current version of the program. :)

### @write ###
Writes the ConceptNetwork in `cn.pkl`, in the current directory, **and** the ConceptNetworkState in `username_state.pkl`, in the same directory.

### @shownodes ###
This command displays the nodes of the ConceptNetwork, as in the ConceptNetworkModule.

This won't display anything unless there are nodes in the ConceptNetwork.
A simple manner to add nodes, is to talk to Ector, naturally.

Example:
```
User>Hi Ector, how are you?
Ector> Hi User, how are you?
User>@shownodes
       how (   token): 1 (0,1,0)
        Hi (   token): 1 (1,0,0)
Hi @bot@, how are you? (sentence): 1 (0)
         , (   token): 1 (0,1,0)
     @bot@ (   token): 1 (0,1,0)
      User ( utterer): 1 (2008/12/11)
         ? (   token): 1 (0,0,1)
       are (   token): 1 (0,1,0)
       you (   token): 1 (0,1,0)
User>
```

**Warning**: this could overwhelm the screen, if your ConceptNetwork is already big!

**Note**: at the launch, Ector try to read the `cn.pkl` file. If you already wrote it, the ConceptNetwork shall not be empty.

### @showlinks ###
This command displays the links of the ConceptNetwork, like in ConceptNetworkModule.

Though it is useful to debug and understand how Ector works, you should not use it, as the output is long.

Example:
```
User>Hi Ector, how are you?
Ector> Hi User, how are you?
User>@showlinks
Hi @bot@, how are you? ------(100, 1)------->          ,
     @bot@ ------(100, 1)-------> Hi @bot@, how are you?
         , ------(100, 1)-------> Hi @bot@, how are you?
Hi @bot@, how are you? ------(100, 1)------->        how
       how ------(100, 1)-------> Hi @bot@, how are you?
       how ------(100, 1)------->        are
        Hi ------(100, 1)------->      @bot@
Hi @bot@, how are you? ------(100, 1)------->        you
         , ------(100, 1)------->        how
Hi @bot@, how are you? ------(100, 1)------->      @bot@
       you ------(100, 1)-------> Hi @bot@, how are you?
        Hi ------(100, 1)-------> Hi @bot@, how are you?
      User ------(100, 1)-------> Hi @bot@, how are you?
     @bot@ ------(100, 1)------->          ,
Hi @bot@, how are you? ------(100, 1)------->       User
         ? ------(100, 1)-------> Hi @bot@, how are you?
       you ------(100, 1)------->          ?
       are ------(100, 1)------->        you
       are ------(100, 1)-------> Hi @bot@, how are you?
Hi @bot@, how are you? ------(100, 1)------->          ?
Hi @bot@, how are you? ------(100, 1)------->        are
Hi @bot@, how are you? ------(100, 1)------->         Hi
User>
```

### @showstate ###
This command displays the state of the nodes of the ConceptNetwork,
corresponding to the utterer, like in ConceptNetworkModule.

NOTE: Though it is useful to debug and understand how Ector works, you
should not use it, as the output is long.

Example:
```
User>Hi Ector, how are you?
Ector >Hi User, how are you?
User>@showstate
oldav	av	age	Node
97	93	2	how(token)
97	90	2	Hi(token)
92	84	2	Hi @bot@, how are you?(sentence)
97	93	2	,(token)
97	90	2	@bot@(token)
82	65	2	User(utterer)
97	93	2	?(token)
97	90	2	are(token)
97	93	2	you(token)
```

### @cleanstate ###
This command, mainly aimed at debugging, can be used to clean the state
from non-activated nodes. It is much more readable when @showstate
display fewer nodes.

Example:
```
User>But you don't have a mouth!
Ector> Don't have a mouth!
User>@showstate
oldav	av	age	Node
76	65	4	Yes, you speak loudly ;)(sentence)
52	24	6	me(token)
0	0	0	already(token)
39	11	6	In fact, I did.(sentence)
0	0	0	I(token)
97	93	2	mouth(token)
19	0	0	User(utterer)
39	11	6	Did you hear me?(sentence)
0	0	0	?(token)
0	0	0	What can we talk about, now?(sentence)
0	0	0	chatterbots(token)
0	0	0	fine(token)
0	0	0	You're welcome.(sentence)
52	24	6	fact(token)
0	0	0	What(token)
43	14	6	Did(token)
0	0	0	can(token)
97	90	2	But(token)
0	0	0	that(token)
0	0	0	could(token)
0	0	0	Hi @bot@, how are you?(sentence)
0	0	0	Yes, I could.(sentence)
58	7	4	,(token)
52	24	6	.(token)
79	65	4	loudly(token)
0	0	0	You already said that.(sentence)
0	0	0	thanks(token)
85	72	4	;)(token)
6	0	0	how(token)
34	0	0	'(token)
0	0	0	any(token)
0	0	0	speak(token)
0	0	0	about(token)
92	84	2	But you don't have a mouth!(sentence)
97	90	2	don(token)
0	0	0	now(token)
0	0	0	Well, we could speak about chatterbots, couldn't we?(sentence)
34	0	0	!(token)
0	0	0	I'm fine, thanks you.(sentence)
97	90	2	a(token)
0	0	0	m(token)
34	0	0	have(token)
0	0	0	it(token)
0	0	0	@bot@(token)
43	14	6	hear(token)
0	0	0	welcome(token)
0	0	0	talk(token)
34	0	0	t(token)
34	0	0	you(token)
0	0	0	re(token)
0	0	0	Hi(token)
0	0	0	we(token)
0	0	0	are(token)
0	0	0	Don't you have any idea?(sentence)
0	0	0	couldn(token)
0	0	0	I know that, you already said it!(sentence)
0	0	0	Well(token)
0	0	0	said(token)
43	14	6	did(token)
0	0	0	Don(token)
9	0	0	Yes(token)
0	0	0	idea(token)
0	0	0	know(token)
43	14	6	In(token)
0	0	0	You(token)
User>@cleanstate
User>@showstate
oldav	av	age	Node
76	65	4	Yes, you speak loudly ;)(sentence)
52	24	6	me(token)
39	11	6	In fact, I did.(sentence)
97	93	2	mouth(token)
39	11	6	Did you hear me?(sentence)
52	24	6	fact(token)
43	14	6	Did(token)
97	90	2	But(token)
58	7	4	,(token)
52	24	6	.(token)
79	65	4	loudly(token)
85	72	4	;)(token)
92	84	2	But you don't have a mouth!(sentence)
97	90	2	don(token)
97	90	2	a(token)
43	14	6	hear(token)
43	14	6	did(token)
43	14	6	In(token)
User>
```



### @log ###
This command change the way the log is taken, in two manners:

  1. change the file in which the log is automatically written
  1. stop the logging, giving no filename, or using `@logoff`

Example:
```
User>@log
Log off (ector.log)
```
The logging off display the last log file name.

To log on, or change the name of the log:
```
User>@log test.log
Log file: test.log
```

### @status ###
The status command display the nodes of the ConceptNetwork, and the name of the states that were created:

```
User>@status
       how (   token): 1 (0,1,0)
        Hi (   token): 1 (1,0,0)
Hi @bot@, how are you? (sentence): 1 (1)
       bot (   token): 1 (0,1,0)
         , (   token): 1 (0,1,0)
      User ( utterer): 1 (2008/11/11)
         ? (   token): 1 (0,0,1)
       are (   token): 1 (0,1,0)
       you (   token): 1 (0,1,0)
States (1)
	User
```

### @sentence [on|off] ###
Set sentence mode on or off.
When the sentence mode is on, Ector thinks a bit about what you said, and then
picks one sentence among those he has already heard.

Using `@sentence` without any argument gives the current sentence mode.

### @generate [on|off] ###
Set generate mode on or off.
When the generate mode is on, Ector thinks a bit about what you said, and then
generates a sentence from one of its activated tokens (usually, a word you used
in the previous sentence).
This generation is a contextually statistical one: likelihood of a word after
one another is taken into account, but activation of the word too.

Activation means concepts that are in the thinking process of Ector (concepts being
sets of tokens).

Using `@generate` without any argument gives the current generate mode.