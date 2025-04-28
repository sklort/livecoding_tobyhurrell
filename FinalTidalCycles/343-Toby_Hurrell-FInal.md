# Second TidalCycles Patch
## Toby Hurrell
## MTEC-343 - Live Coding

```javascript
-- ***********
-- beat ******
-- ***********


-- gooofy one shot

once $ s "finalSamples:5"
  # gain (1.5)

-- goofy loop
d8 $ slice 3 "<0*2 ~ 1 2>"
  $ s "finalSamples:5"
  # gain (1.5)
  -- #silence
 -- "<0*2 ~ 1 2>"
-- ****************************
-- kicks

d1 $ fast 1 $ s "[gabba gabba gabba gabba*2 | gabba gabba gabba gabba]"
  # distort 0.25
  # shape 0.25
  # gain (0.9)
  -- # silence

d1 $ fast 1 $ s "[gabba gabba gabba gabba*2 | gabba gabba gabba gabba]"
-- "[gabba ~ gabba ~]" "[gabba ~ ~ ~ ]" "<[gabba*2 gabba gabba gabba*2] [gabba gabba gabba gabba]>" "[gabba gabba gabba gabba*2 | gabba gabba gabba gabba]"
  # crush "[16 | 12 | 8]"
  # triode "<0 0.5 0.75 0.5>"
  # distort (0.75)
  # shape "<0 0.25 0.5 0.75 0.5 0.25>"
  # coarse "[1 | 2 | 3 | 4 | 6 | 8]"
  # gain (1)
  -- # silence


d1 $ s "[reverbkick reverbkick reverbkick reverbkick*2 | reverbkick reverbkick reverbkick reverbkick]"
  # shape "[0 | 0.5]"
  # distort "[0.25 | 0.5 | 0.75]"
  # crush "[16 | 12 | 8]"
  # gain (1)
  -- # squiz "[2 | 4 | 8]"
  -- # silence

  d1 $ s "<[909 909 909 909] [909 909 909 909*2]>"
    # distort 0.75
    # shape 0.5
    # gain (1.2)
    -- # silence



-- hh
d2 $ fast 1 $ s  "~ [808oh | 808oh*2] ~ 808oh ~ [808oh | 808oh*2 | 808oh*4] ~ 808oh"
  # shape "<0.6 0.9>"
  # distort "<0.75 1>"
  # crush "<16 12 10 8>"
  # gain (0.85)
  -- # room 0.5
  -- # size 0.8
  -- # lpf 2000
  -- # silence

-- "~ 808oh"
  -- "~ 808oh ~ 808oh ~ 808oh ~ 808oh"
  -- "~ [808oh | 808oh*2] ~ 808oh ~ [808oh | 808oh*2 | 808oh*4] ~ 808oh"
  -- "~ ~ ~ 808oh ~ ~ ~ 808oh"


-- claps
d3 $ fast 1 $ s "[~ cp cp cp ~ cp cp cp*2]"
  # squiz "[2 | 4 | 8]"
  # shape "[0.2 | 0.5 | 0.7]"
  # distort "[0.3 | 0.6]"
  # crush "[16]"
  # gain (0.8)
  -- # lpf 500
  -- # silence

-- "~ ~ [cp | ~] [~ | cp] ~ ~ [~ | cp] ~"
-- "[~ ~ cp*2 ~ ~ cp cp cp]"
-- "[~ cp cp cp ~ cp cp cp*2]    "[~ ~ cp*2 ~ ~ cp cp cp]"

-- noise
d4
  $ fast "<1 1 2 2>"
  $ degradeBy 0.5
  $ segment "<4 8 16>"
  $ n (scale "major" $ floor <$> (range 0 24 rand))
    # s "supernoise"
    # octave "[4 | 5 | 6]"
    # squiz "<4 8 12 16>"
    # distort "[0 | 0.3 | 0.5]"
    # gain (1.15)
    -- # silence

-- the tickler
d5 $ degradeBy 0.5 $ fast 4 $ note (arp "[converge | diverge | thumbup | pinkyup]" "<f'sevenSharp5flat9>")
  # speed (rand*12)
  # octave "[3 | 4 | 5]"
  # sound "superhoover"
  # crush "[3 | 2 | 1]"
  # distort "[0 | 0.3 | 0.5 | 0.75 | 1]"
  # coarse "[4 | 6 | 8 | 16]"
  # lpf 10000
  # freeze "[0 | 0.5 | 1 | 2]"
  -- # silence





-- ***********
-- jodler*****
-- ***********




d6 $ loopAt 4
  $ s "finalSamples:1"
    # gain 1.2
    -- # silence

d6 $ loopAt 4
  $ s "finalSamples:2"
    # gain 1.2
    -- # silence

d6
  $ fast 1 $ loopAt 8
  -- $ slow 2 $ slice 8 "<1 4 7>" $ segment 1
  $ s "finalSamples:3"
    # gain 1.2
    # fshift (0)
    # squiz 0
    # distort 0
    -- # silence

d6
  $ fast 1 $ loopAt 8
  -- $ slow 2 $ slice 8 "<1 4 7>" $ segment 1
  $ s "finalSamples:4"
    # gain 1.2
    # fshift (0)
    # squiz 0
    # distort 0
    -- # silence

-- ambient into beat
d6 $ fast 2 $ loopAt 8  $ randslice "[2 | 3 | 4 | 5]"
  $ s "finalSamples:0"
    -- # gain 1.2
    # gain 1
    # dry 0.0
    # smear 1
    # delay 0.5
    # freeze 1
    # lpf 300
    # room 0.8
    # size 0.95
    -- # silence



-- *********
-- ambient
-- ***********



-- tones
d11
  $ degradeBy 0.20
  $ slow 1
  $ freq "[136 | 283 | 403 | 639 | 1029 | 1830]"
    # gain 0.9
    # s "superfork"
    # rel 1000
    # attack "[0 | 2.5 | 5]"
    # accelerate "[0 | 0.1 | 0.3 | 0.5]"
    # room 0.85
    # dry 0
    # size 0.85
    # crush "[12 | 10 ]"
    # lpf 2000
    # fshift (-200)
    -- # silence

-- keyboard
d9
  $ degradeBy 0.5
  $ slow "[8 | 12 | 16]" $ s "toys" <| n (run 13)
      # fshift (rand * 1000)
      # smear "[0.5 | 1 | 2]"
      # squiz "[0 | 2 | 4]"
      # lpf 6000
      # room 0.75
      # dry 0
      # size 0.8
      # gain 0.6
      -- # silence

-- high blips
d10
  $ slow 1
  $ s "birds"
    # squiz "[2 | 4 | 8 | 16 | 32]"
    # fshift (rand * 5000)
    # freeze (5)
    # room 0.5
    # size 0.5
    # smear "[1 | 2 | 3 | 4 | 5]"
    # delay 0.5
    # delayt "[200 | 300 | 400]"
    # delayfb 0.3
    # gain "[0.5 | 1 | 1.5]"
    -- # silence

d12
  $ degradeBy 0.25
  $ slow "[16 | 20 | 24]"
  $ s "alphabet" <| n (shuffle 8 $ run 26)
    # dry 0.25
    # gain 0.6
    # squiz "[0 | 0 | 2 | 4]"
    # freeze 5
    # delay 1
    # delayt "[300 | 400 | 500 | 600]"
    # delayfb "[0.3 | 0.4 | 0.5 | 0.6]"
    # smear "[0 | 0.5 | 1 | 2]"
    # crush "[16 | 12 | 8 | 4]"
    # room 0.7
    # size 0.9
    -- # silence


  hush

  panic


setcps (190/60/4)

```
I've been listening to a lot of hardcore and also yodeling for some reason (i don't know why), so I wanted to combine my first patch with some yodeling. I thought it'd be funny but also kinda groovy...
I started out by editing samples in Ableton, and then importing them into TidalCycles and making sure they synced up with the project.
I then started making edits to get the beat and yodels to sync up better, along with some creative edits for both.
I wanted to have a smooth intro into this, as I thought five minutes of this stupidness would be a bit too much.
I took the yodeling sample, slowed it down, smeared and froze it as the foundation of my ambience. I added some more elements I had been working on before to come in out and of this intro, and to transition to the beat I simply dialed down the smear and went back to the original temple for the yodel. 
