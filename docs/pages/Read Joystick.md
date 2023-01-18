# Read the Joystick

Uses OSBYTE &80:

In:

X = 0 Read Fire Buttons Return value in X

X = 1 Read X Axis Return value in Y;X ( Returns 0 - 65535 Right Low, Left High )

X = 2 Read Y Axis Return value in Y;X ( Returns 0 - 65535 Down Low, Up High )

## The Code

    JOY_RIGHT        = 1
    JOY_LEFT           = 2
    JOY_DOWN        = 4
    JOY_UP      = 8
    JOY_FIRE            = &10

    JoyBits             = &70


    ._READ_JOYSTICK:
        LDA     #&00
        STA     JoyBits

    .left_right:
        LDX #1
        LDA     #&80
        JSR     _OSBYTE
        LDA #0
        CPY     #&25
        BCS     not_right
        ORA     #JOY_RIGHT
    .not_right:
        CPY     #&DB
        BCC     not_left
        ORA     #JOY_LEFT
    .not_left:
        STA     JoyBits

    .up_down:
        LDX     #&02
        LDA     #&80
        JSR     _OSBYTE
        LDA     JoyBits
            CPY     #&25
        BCS     not_down
        ORA     #JOY_DOWN
    .not_down:
        CPY     #&DB
        BCC     not_up
        ORA     #JOY_UP
    .not_up:
        STA     JoyBits

            LDX     #&00
        LDA     #&80
        JSR     _OSBYTE
        TXA
        LSR     A
        BCC     not_fire

        LDA     JoyBits
        ORA     #JOY_FIRE
        STA     JoyBits

    .not_fire:
        RTS
