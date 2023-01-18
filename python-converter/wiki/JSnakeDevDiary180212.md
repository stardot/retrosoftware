## JSnake Dev Diary 18/02/2012

[&lt;----Back to JSnake Dev Diary Index](JSnakeDevDiary "wikilink")

I started from scratch a couple of weeks back. This first entry is a review of where I've got to thus far. I daresay subsequent entries may be more brief as the changes will likely be smaller, incremental steps.

#### First steps: plotting pixels to the screen

It seems to me that both the pleasure and the pain of coding in assembler is that everything is done in tiny baby steps, i.e. it often takes a long series of (short) 6502 assembler instructions to accomplish something, whereas in a high level language, only one or two lines of code may be needed to do the same thing. I found myself returning to this thought many times as I worked out my first goal: plotting a series of pixels to the screen in a horizontal line. Yes, it's a very humble goal, but I've found that taking many small steps has resulted in achievable results, which gives me incentive to continue.

I learned that MODE 2 would likely be the easiest mode to use to move pixels around the screen. Why? Because in MODE 2, a byte in screen memory represents two pixels.. so you ought to be able to move two pixels at a time by manipulating bytes. It's genereally easier (and quicker) to add and subtract bytes than it is to manipulate bits in a byte.

Kees van Oss succintly describes MODE 2 and 5 pixels in his dev diary for Atom Galaforce. I've borrowed his diagram to illustrate:

![](./images/Colours.PNG "Colours.PNG")

His full dev diary for Atom Galaforce can be found at: <http://www.retrosoftware.co.uk/wiki/index.php/GalaforceAtomDevDiary>

Before even writing any assembler, to test the idea that simply storing a value in memory would result in pixel/s being drawn on the screen, I typed this:

<tt>

`>MODE 2`

`> ?&4000=&0C`

</tt>

This will plot two green pixels (horizontally) to the screen.

I then read about Beeb screen addressing with horror. Knowing that MODE 2 is a 20K screen mode starting at &3000, ending at &7FFF - I foolishly assumed that addressing would simply be consecutive bytes starting from top left of screen until bottom right is reached.. ie top line of screen would be &3000 to &304F, 2nd line &3050 to &30A0 etc. Sadly, it's more complicated. Instead, BBC screen modes (apart from 7) are based on a series of 8x8 pixel blocks running horizontally, left to right (and then on to the next row) from the top left of the screen down to the bottom right. This is because the 6845 CRTC video chip used by the BBC is primarily designed to display 8x8 pixel characters. This is a pain if I want to move a set of pixels across the screen as I can't simply add one to an address each time I want to write to a pixel to the right, for example.

This is illustrated below, where I want to write 8 pixels to the screen. Each box represents 8x8 bytes in MODE2, where each byte stores 2 pixels. Note that screen addressing in MODE2 starts at &3000, top left, but I've start at 0 for clarity. See how in this case, to plot 8 pixels I'd have to write to addresses 26, 27, 60 and 61. Not nice.

![](./images/Mode2 screen address layout 8pixels.png "Mode2_screen_address_layout_8pixels.png")

To make life easier, a handy routine could be written to return a screen address derived from X and Y coordinate input parameters (similar to the PLOT or DRAW BASIC instructions). Being such a newbie to 6502 I wasn't thrilled at the prospect of trying to work out such a routine at this stage. Fortunately, both assembler books I have referenced have such routines. Further, Steve O'Leary has written some liberally commented assembler routines that handle this issue and published it in the Sample Code section of this site: <http://www.retrosoftware.co.uk/wiki/index.php/Calculate_Screen_Address>

I chose to use Steve's code as it was more generic and easier to use than the examples in the assembler books - but the actual text in chapters 7 and 10 of "Mastering Assembler" and chapter 10 of "Creative assembler" are well worth the read for a very full explanation of screen addressing which helped me better understand Steve's routine.

Using Steve's Screen Address routine.. I was soon able to progress to these giddy heights:

![](./images/Greenline.png "Greenline.png")

#### Moving the snake around the screen

As mentioned earlier, I'm progressing in small steps.. so I'm not using sprites just yet. All I'm doing is plotting a 2x3 blob of green pixels to screen, as per this code snippet:

<tt>

                    jsr ScreenStartAddress

            lda #&0C ; &0C = 2 green pixels

            eor (XYScreenAddress,X) : sta (XYScreenAddress,X); EOR &0C with contents of (screen)address. Store (i.e plot) result to screen address

            sta snakehead_scrn_addr ; store EORed result of plotted pixel - ie it's colour. If it is green (&0C), no collision, otherwise, we have a collision.

            inc YOrd

            jsr ScreenStartAddress



            lda #&0C

            ldx #0

            eor (XYScreenAddress,X) :sta (XYScreenAddress,X)

            sta snakehead_scrn_addr+1



            inc YOrd

            jsr ScreenStartAddress

            lda #&0C

            ldx #0

            eor (XYScreenAddress,X) : sta (XYScreenAddress,X)

            sta snakehead_scrn_addr+2

            dec YOrd

            dec YOrd

</tt>

So to move the snake, I have a routine called Move, which contains the above snippet. Move is called repeatedly from a loop. The snake is just a series of 2x3 pixel blobs which are plotted using above code.

The snake moves in increments of 2 pixels. The easiest way to animate the snake movement is to append a "new" head (pixel blob) to the existing one, and erase the tail pixel blob. I've reserved 256 bytes in memory (I may yet need more, but for now 256 bytes is easy to work with) to store X and Y ords for each pixel blob that forms part of the snake. This means I can store up to 128 X,Y coord pairs, each representing the top left pixel of a 2x3 blob.

The 256 bytes are used as a circular list. I have a snake tail pointer and the snake head pointer, which point to the addresses in the list that record the X and Y coords of the tail pixel blob and head pixel blob. This way, it easy for the Move routine to look up and update tail and head locations.

#### Collision detection

Once I had the snake moving around the screen, I also created (and cribbed) some more routines. I nabbed some of the keyboard routine from [HyperViper](http://www.retrosoftware.co.uk/wiki/index.php/HyperViper) and plotted some food to the screen. The food is currently a yellow square :)

Next, I need collision detection to check for:

- collision with self

- collision with food

- collision with screen boundaries

The routine probably needs updating. I've checked collision in two ways -

- I check the resultant colour of the head pixels following the EORing of head pixels to screen. If green, no collision (the snake is green), if red then collision with food, otherwise collision with self. If none of the above, then on to next collision check

- Check to see if snake head touches screen boundaries by comparing x,y ord of head with ords of screen edges

Routine is shown below. Would welcome critique from the experts amongst us (be gentle though :) )

<tt>

    ldx #3

        .CollisionLoop

            dex

            lda snakehead_scrn_addr, X



            cmp #&0C ; head is green - no collision

            beq decCLcounter

            cmp #&03 ; check if head has hit yellow - collision with food

            bne CheckSelf



            lda #HitFood

            sta CollisionState

            rts



            .CheckSelf

            lda #HitSelf

            sta CollisionState



            rts



            .decCLcounter

            txa

        bne CollisionLoop

        jmp therest ; no  collisions to food or self so jmp to more checks





        .therest    ; check for collision with scrn boundary

            dec snakehead_ptr

            lda (snakehead_ptr,X)

            cmp #LBound

            beq CDEnd

            cmp #RBound

            beq CDEnd





            inc snakehead_ptr

            lda (snakehead_ptr,X)

            cmp #UBound ; problem here - each snake seg is 3 pixels deep.. so when snake moves up, y Ord is decreased by 3.. which means when we

            beq CDEnd

            cmp #BBound-3

            beq CDEnd



            lda #HitNothing

            sta CollisionState

            rts



            .CDEnd



            lda #HitScrnBoundary

            sta CollisionState

    rts

</tt>

#### Taking stock. Pseudocode to plan the rest of the code

At this point, I thought I'd better plan the rest of the routines I'd be needing. Here it is for better or for worse.

<tt>

    First draft pseudocode with approximate structure and routines.  Routines with * are those that I haven't started on yet



    .GameState

    {

        jsr.StartScreen*

        jsr .InGame

        jsr .HiScore*







        .Ingame

        {

            jsr Init

            jsr SnakeLive



            .Init

            {

                jsr SetupGameScreen

                jsr Draw Boundary *

                jsr Draw Banner *

                jsr Init Snake

                jsr Init Score *

                jsr Plot Food

            }





            .SnakeLive

            {

                .SnakeMoving

                {

                    jsr.Keypress

                    jsr .Move

                    jsr .Collision Detect

                    If Food,

                        jsr .EatFood.

                        jsr .GrowSnake

                        jsr .UpdateScore*

                        jsr .UpdateBanner*



                (loop if no collision

                }

                jsr .Crash

                dec Lives

                jsr Update banner*



            }

        (loop around Ingame until Lives = 0)

        }

    }

    jmp Gamestate (ie after Hiscore table, go back to opening "welcome" screen of game)





    .Draw Boundary*

    .Draw Banner*



    .EatFood*

    .UpdateScore*

    .UpdateBanner*

    .RandomNumber



    .PlotFood

    .Crash *

     <do a check to make sure food not colliding with anything before it is plotted>

    .HiScore *



</tt>

[&lt;----Back to JSnake Dev Diary Index](JSnakeDevDiary "wikilink")
