# `tab` - Put Music in Your Hands!

Tab is a tiny command-line utility to render tablatures for numerous music instruments.

![Screenshot](/screenshot.png)

## Features

* Supports **every** tablature notation! Over 25 instruments in a single binary.
    * [Guitar tabs](https://en.wikipedia.org/wiki/Tablature#Guitar_tablature) for the following instruments:
        * **Guitar** (6-string, standard tuning)
        * **Ukulele** (standard GCEA tuning)
        * **Mandolin** (standard GDAE tuning)
        * **Violin** (standard GDAE tuning, with position markers)
        * [Cigar Box Guitar](https://en.wikipedia.org/wiki/Cigar_box_guitar) (GDg open tuning)
        * [Diddley Bow](https://en.wikipedia.org/wiki/Diddley_bow) (1-string and 2-string in G+D and G+C tunings)
    * [Harmonica tabs](https://en.wikibooks.org/wiki/Harmonica/Tablature)
        * Diatonic harmonica (key of C and D)
        * Chromatic harmonica
    * [Klavarscribo](https://en.wikipedia.org/wiki/Klavarskribo) (piano roll notation)
        * 48-key Piano
        * 25-key Toy Piano
    * [Kalimba tabs](https://www.kalimbaclasses.com/kalimba-guides/how-to-read-number-tabs)
        * 17-key Kalimba
        * 21-key Kalimba
    * [Flutes / Wind instruments](https://www.whistletabs.com/)
        * Recorder (German and Baroque/English fingering systems)
        * Irish Tin Whistle in D
        * Native American Flute in A (4-hole, 5-hole, and 6-hole)
        * Pendant Ocarina (4-hole)
        * Xaphoon (Pocket Sax) in C
        * Trumpet in Bb
        * Alto Saxophone in Eb
    * [Jianpu](https://en.wikipedia.org/wiki/Numbered_musical_notation)
        * Chinese Numeric Notation (1 2 3 4 5 6 7) for any instrument
* Great for self-taught musicians and amateurs, also kid-friendly — comes with 9 kids songs ready to play!
* Allows to **transpose** music by any number of semitones for the most convenient key.
* Uses visually appealing **colored unicode output** with automatic terminal detection, with **ASCII** fallback and **NO_COLOR** support.
* Adjustable **padding** for comfortable reading.
* **Tiny** — single C file, no external dependencies, builds in under a second on any machine!

## Usage

It's easy to build and install `tab` from sources:

```
$ git clone https://github.com/zserge/tab
$ cd tab
$ make
$ ./tab -i uke examples/ode_to_joy.abc

    A│-------------0---│---0---------------│-------------------│-------------│-
    E│-2---2-----------│-----------2---0---│-----------0---2---│---2-0---0---│-
    C│-----------------│-------------------│---2---2-----------│-------------│-
    g│---------0-------│-------0-----------│-------------------│-------------│-
    w: Freu-de, schö-ner Göt-ter-funk-en, Toch-ter aus E-ly-si-um,
    ...
```

### Options

| Flag | Description |
|------|-------------|
| `-i NAME` | Select instrument (see list below) |
| `-t NUM` | Transpose by NUM semitones (-24..+24) |
| `-c` | Force colored output |
| `-C` | Disable colored output |
| `-a` | Disable unicode (use ASCII symbols) |
| `-p NUM` | Set left padding (0..99, default 2) |
| `-h` | Show help and available instruments |

### All supported instruments

| Name | Instrument |
|------|------------|
| `guitar` | 6-string Guitar Tabs |
| `uke` | Ukulele Tabs |
| `mandolin` | Mandolin Tabs |
| `violin` | Violin Tabs (with position markers) |
| `cbg` | Cigar Box Guitar (GDg tuning) |
| `diddley` | Diddley Bow / Unitar (1-string) |
| `2gd` | Two-string Diddley Bow (G+D) |
| `2gc` | Two-string Diddley Bow (G+C) |
| `recorder` / `german` | Recorder (German System) |
| `baroque` / `english` | Recorder (Baroque/English System) |
| `whistle` | Irish Tin Whistle in D |
| `xaphoon` | Xaphoon (Pocket Sax) in C |
| `pendant` | Pendant Ocarina (4-hole) |
| `naf` / `naf6` | Native American Flute in A (6-hole) |
| `naf5` | Native American Flute in A (5-hole) |
| `naf4` | Native American Flute in A (minor pentatonic, 4-hole) |
| `trumpet` | Trumpet in Bb |
| `sax` | Alto Saxophone in Eb |
| `harp` / `diatonic` | Diatonic Harmonica |
| `chromatic` | Chromatic Harmonica |
| `piano` | Klavarscribo for 48-key piano |
| `toy` | Toy 25-key piano |
| `kalimba` | Kalimba (17 keys) |
| `kalimba21` | Kalimba (21 keys) |
| `jianpu` / `123` | Chinese Numeric Notation |

### Kids songs included

The `examples/kids/` directory contains ready-to-play songs:

```
twinkle.txt         Twinkle Twinkle Little Star
oldmacdonald.txt    Old MacDonald Had a Farm
mary_had_a_little_lamb.txt
london_bridge.txt   London Bridge Is Falling Down
itsy_bitsy_spider.txt
wheels_on_the_bus.txt
rowyourboat.txt     Row, Row, Row Your Boat
happybirthday.txt   Happy Birthday
yankee_doodle.txt   Yankee Doodle
```

Try them out:
```
$ ./tab -i recorder examples/kids/twinkle.txt
```

## Input format

Tab works well with [ABC notation](https://abcnotation.com/) but you may use a simplified text notation, too.

Tab operates over a range of 4 octaves from C3 to B6. This is sufficient for most instruments that use tablature music notation.

Notes are written as letters (`CDEFGAB` for octave 4 and `cdefgab` for octave 5). Notes in octave 3 are followed by `,` and notes in octave 6 are followed by `'`. Technically, octaves can be lowered and raised even further, but most instruments won't be able to display such tabs correctly.

Like in ABC notation, notes may be prefixed by `^` to make them sharp and `_` to make them flat. You may alternatively write `#` after the note to make it sharp.

White space is preserved, and `|` is rendered as a bar separator. The rest of the ABC notation is ignored.

Lines that do not contain a musical notation are rendered verbatim as plain text.

## Examples

Here is some sample input:

```
Here are C notes in 4 octaves:
C, C c c'
And here is a E minor scale:
E F# G A | B c d e
```

Rendered for a Tin Whistle you may see something like this:

```
    Here are C notes in 4 octaves:
    x   x   ○   ○
    x   x   ●   ●
    x   x   ●   ●
    x   x   ○   ○
    x   x   ○   ○
    x   x   ○   ○
    x   x       +
    And here is a E minor scale:
    ●   ●   ●   ●   │   ●   ○   ○   ●
    ●   ●   ●   ●   │   ○   ●   ●   ●
    ●   ●   ●   ○   │   ○   ●   ●   ●
    ●   ●   ○   ○   │   ○   ○   ●   ●
    ●   ○   ○   ○   │   ○   ○   ●   ●
    ○   ○   ○   ○   │   ○   ○   ●   ○
                    │               +
```

In Numeric notation (Jianpu) it would look like:

```
    Here are C notes in 4 octaves:
          .  :
    1  1  1  1
    *
    And here is a E minor scale:
                       .  .  .
    3  ♯4  5  6  |  7  1  2  3
```

And for Cigar Box Guitar it would become:

```
    Here are C notes in 4 octaves:
    g│-x-------5---17-
    D│-x--------------
    G│-x---5----------
    And here is a E minor scale:
    g│---------0---2---│---4---5---7---9-
    D│-2---4-----------│-----------------
    G│-----------------│-----------------
```

## Finding and downloading ABC notation

The `contrib/` directory includes `abc-get`, a helper script to search and download ABC notation from [thesession.org](https://thesession.org) — a large collection of traditional Irish and folk tunes.

```
$ ./contrib/abc-get -l "ode to joy"
Searching for: ode to joy
Found 5 tune(s)
  1. Ode To Joy (march)
  2. Ode To Joy (waltz)
  3. Wandering Oileán Óir (slide)
  4. Ochón a Dhonncha (song)
  5. Kilmovee (polka)

Enter tune number to download [1-5] (or 0 to cancel): 1
Fetching: Ode To Joy...
Saved to Ode_To_Joy.abc
Tip: run ./tab -i <instrument> "Ode_To_Joy.abc" to see the tablature
```

Pipe directly into `tab` without saving to a file:
```
$ ./contrib/abc-get -n 1 "ode to joy" | ./tab -i whistle
```

### Options

| Flag | Description |
|------|-------------|
| `-l` | List matching tunes and download interactively |
| `-n N` | Select tune number N (default: 1) |
| `-h` | Show help |

## Contributing

Contributions to Tab are welcome! Whether you want to report a bug, request a feature, or submit a pull request, please feel free to get involved.

Tab is open-source software licensed under the [MIT License](/LICENSE).
