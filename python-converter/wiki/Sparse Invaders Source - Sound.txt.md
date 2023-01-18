# Sparse Invaders Source - Sound.txt

`   ;-------------------------------------------------------------------------------`
`   ;  Sound  - Invaders ...`
`   ;  Written by PJ for use within Invaders.`
`   ;`
`   ;  Copyright 2008,2009 Neil Beresford`
`   ;`
`   ;    This file is part of Sparse Invaders.`
`   ;    Sparse Invaders is free software: you can redistribute it and/or modify`
`   ;    it under the terms of the GNU General Public License as published by`
`   ;    the Free Software Foundation, either version 3 of the License, or`
`   ;    (at your option) any later version.`
`   ;`
`   ;    Sparse Invaders is distributed in the hope that it will be useful,`
`   ;    but WITHOUT ANY WARRANTY; without even the implied warranty of`
`   ;    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the`
`   ;    GNU General Public License for more details.`
`   ;`
`   ;    You should have received a copy of the GNU General Public License`
`   ;    along with Sparse Invaders.  If not, see <`[`http://www.gnu.org/licenses/`](http://www.gnu.org/licenses/)`>.`
`   ;`
`   ;`
`   ;-------------------------------------------------------------------------------`
`   ;-----------------------------`
`   ;`
`   ;       VDU CODES`
`   ;`
`   ;-----------------------------`
`   .alias VDU_NULL $00`
`   .alias VDU_TO_PRINTER   $01`
`   .alias VDU_ENABLE_PRINTER   $02`
`   .alias VDU_DISABLE_PRINTER  $03`
`   .alias VDU_WRITE_TEXT   $04`
`   .alias VDU_WRITE_TEXT_GFX   $05`
`   .alias VDU_ENABLE   $06`
`   .alias VDU_BEEP $07`
`   .alias VDU_CURSOR_BACK  $08`
`   .alias VDU_CURSOR_FWD   $09`
`   .alias VDU_CURSOR_DOWN  $0A`
`   .alias VDU_CURSOR_UP    $0B`
`   .alias VDU_CLEAR_TEXT   $0C`
`   .alias VDU_RETURN   $0D`
`   .alias VDU_PAGED_MODE_ON    $0E`
`   .alias VDU_PAGED_MODE_OFF   $0F`
`   .alias VDU_CLEAR_GFX    $10`
`   .alias VDU_TEXT_COLOUR  $11`
`   .alias VDU_GFX_COLOUR   $12`
`   .alias VDU_LOGICAL_COLOUR   $13`
`   .alias VDU_DEFAULT_LOGICAL_COLOURS  $14`
`   .alias VDU_DISABLE  $15`
`   .alias VDU_MODE $16`
`   .alias VDU_PROGRAM_DISPLAY_CHAR $17`
`   .alias VDU_GFX_WINDOW   $18`
`   .alias VDU_PLOT $19`
`   .alias VDU_RESTORE_WINDOW   $1A`
`   .alias VDU_ESCAPE   $1B`
`   .alias VDU_TEXT_WINDOW  $1C`
`   .alias VDU_GFX_ORIGIN   $1D`
`   .alias VDU_CURSOR_HOME  $1E`
`   .alias VDU_MOVE_CURSOR  $1F`
`   ;-----------------------------`
`   ;`
`   ;       OSWORD`
`   ;`
`   ;-----------------------------`
`   .alias OSW_READ_LINE    $00`
`   .alias OSW_READ_SYS_CLOCK   $01`
`   .alias OSW_WRITE_SYS_CLOCK  $02`
`   .alias OSW_READ_TIMER   $03`
`   .alias OSW_WRITE_TIMER  $04`
`   .alias OSW_READ_IO_BYTE $05`
`   .alias OSW_WRITE_IO_BYTE    $06`
`   .alias OSW_SOUND    $07`
`   .alias OSW_DEFINE_ENVELOPE  $08`
`   .alias OSW_READ_PIXEL   $09`
`   .alias OSW_READ_CHARACTER_DEFN  $0A`
`   .alias OSW_READ_PALETTE $0B`
`   .alias OSW_WRITE_PALETTE    $0C`
`   .alias OSW_READ_CURSOR  $0D`
`   ;-----------------------------`
`   ;`
`   ;       INKEY`
`   ;`
`   ;-----------------------------`
`   .alias INKEY_SPACE  $9D`
`   .alias INKEY_SLASH_QUESTION $87`
`   .alias INKEY_X  $BD`
`   .alias INKEY_Z  $9E`
`   .alias INKEY_A  $BE`
`   .alias INKEY_COMMA_LESSTHAN $99`
`   .alias INKEY_PERIOD_GREATERTHAN $98`
`   .alias INKEY_RETURN $B6`
`   ;-----------------------------`
`   ;`
`   ;       OSBYTE`
`   ;`
`   ;-----------------------------`
`   .alias FX_PRINT_OPERATING_SYSTEM_VERSION    $00`
`   .alias FX_USER_OSBYTE_CALL_RW_LOCATION_ $01`
`   .alias FX_SELECT_INPUT_STREAM   $02`
`   .alias FX_SELECT_OUTPUT_STREAM  $03`
`   .alias FX_ENABLEDISABLE_CURSOR_EDITING  $04`
`   .alias FX_SELECT_PRINTER_DESTINATION    $05`
`   .alias FX_SET_CHARACTER_IGNORED_BY_PRINTER  $06`
`   .alias FX_SET_RS_BAUD_RATE_FOR_RECEIVING_DATA   $07`
`   .alias FX_SET_RS_BAUD_RATE_FOR_DATA_TRANSMISSION    $08`
`   .alias FX_SET_FLASHING_COLOUR_MARK_STATE_DURATION   $09`
`   .alias FX_SET_FLASHING_COLOUR_SPACE_STATE_DURATION  $0A`
`   .alias FX_SET_KEYBOARD_AUTOREPEAT_DELAY_INTERVAL    $0B`
`   .alias FX_SET_KEYBOARD_AUTOREPEAT_RATE  $0C`
`   .alias FX_DISABLE_EVENTS    $0D`
`   .alias FX_ENABLE_EVENTS $0E`
`   .alias FX_FLUSH_SELECTED_BUFFER_CLASS   $0F`
`   .alias FX_SELECT_ADC_CHANNELS_TO_BE_SAMPLED $10`
`   .alias FX_FORCE_AN_ADC_CONVERSION   $11`
`   .alias FX_RESET_SOFT_KEYS   $12`
`   .alias FX_WAIT_FOR_VERTICAL_SYNC    $13`
`   .alias FX_EXPLODE_SOFT_CHARACTER_RAM_ALLOCATION $14`
`   .alias FX_FLUSH_SPECIFIC_BUFFER $15`
`   .alias FX_READ_VDU_STATUS   $75`
`   .alias FX_REFLECT_KEYBOARD_STATUS_IN_LEDS   $76`
`   .alias FX_CLOSE_ANY_SPOOL_OR_EXEC_FILES $77`
`   .alias FX_WRITE_CURRENT_KEYS_PRESSED_INFORMATION    $78`
`   .alias FX_PERFORM_KEYBOARD_SCAN $79`
`   .alias FX_PERFORM_KEYBOARD_SCAN_FROM__  $7A`
`   .alias FX_INFORM_OS_PRINTER_DRIVER_GOING_DORMANT    $7B`
`   .alias FX_CLEAR_ESCAPE_CONDITION    $7C`
`   .alias FX_SET_ESCAPE_CONDITION  $7D`
`   .alias FX_ACKNOWLEDGE_DETECTION_OF_ESCAPE_CONDITION $7E`
`   .alias FX_CHECK_FOR_EOF_ON_AN_OPEN_FILE $7F`
`   .alias FX_READ_ADC_CHANNEL_OR_GET_BUFFER_STATUS $80`
`   .alias FX_READ_KEY_WITH_TIME_LIMIT  $81`
`   .alias FX_READ_MACHINE_HIGH_ORDER_ADDRESS   $82`
`   .alias FX_READ_TOP_OF_OS_RAM_ADDRESS_OSHWM  $83`
`   .alias FX_READ_BOTTOM_OF_DISPLAY_RAM_ADDRESS_HIMEM  $84`
`   .alias FX_READ_BOTTOM_OF_DISPLAY_ADDRESS_FOR_A_GIVEN_MODE   $85`
`   .alias FX_READ_TEXT_CURSOR_POSITION_POS_AND_VPOS    $86`
`   .alias FX_READ_CHARACTER_AT_CURSOR_POSITION $87`
`   .alias FX_PERFORM_CODE  $88`
`   .alias FX_PERFORM_MOTOR $89`
`   .alias FX_INSERT_VALUE_INTO_BUFFER  $8A`
`   .alias FX_PERFORM_OPT   $8B`
`   .alias FX_PERFORM_TAPE  $8C`
`   .alias FX_PERFORM_ROM   $8D`
`   .alias FX_ENTER_LANGUAGE_ROM    $8E`
`   .alias FX_ISSUE_PAGED_ROM_SERVICE_REQUEST   $8F`
`   .alias FX_PERFORM_TV    $90`
`   .alias FX_GET_CHARACTER_FROM_BUFFER $91`
`   .alias FX_READ_FROM_FRED__MHZ_BUS   $92`
`   .alias FX_WRITE_TO_FRED__MHZ_BUS    $93`
`   .alias FX_READ_FROM_JIM__MHZ_BUS    $94`
`   .alias FX_WRITE_TO_JIM__MHZ_BUS $95`
`   .alias FX_READ_FROM_SHEILA_MAPPED_IO    $96`
`   .alias FX_WRITE_TO_SHEILA_MAPPED_IO $97`
`   .alias FX_EXAMINE_BUFFER_STATUS $98`
`   .alias FX_INSERT_CHARACTER_INTO_INPUT_BUFFER    $99`
`   .alias FX_WRITE_TO_VIDEO_ULA_CONTROL_REGISTER_AND_COPY  $9A`
`   .alias FX_WRITE_TO_VIDEO_ULA_PALETTE_REGISTER_AND_COPY  $9B`
`   .alias FX_RW__CONTROL_REGISTER_AND_COPY $9C`
`   .alias FX_FAST_TUBE_BPUT    $9D`
`   .alias FX_READ_FROM_SPEECH_PROCESSOR    $9E`
`   .alias FX_WRITE_TO_SPEECH_PROCESSOR $9F`
`   .alias FX_READ_VDU_VARIABLE_VALUE   $A0`
`   .alias FX_READ_START_ADDRESS_OF_OS_VARIABLES_LOW_BYTE   $A6`
`   .alias FX_READ_START_ADDRESS_OF_OS_VARIABLES_HIGH_BYTE  $A7`
`   .alias FX_READ_ADDRESS_OF_ROM_POINTER_TABLE_LOW_BYTE    $A8`
`   .alias FX_READ_ADDRESS_OF_ROM_POINTER_TABLE_HIGH_BYTE   $A9`
`   .alias FX_READ_ADDRESS_OF_ROM_INFORMATION_TABLE_LOW_BYTE    $AA`
`   .alias FX_READ_ADDRESS_OF_ROM_INFORMATION_TABLE_HIGH_BYTE   $AB`
`   .alias FX_READ_ADDRESS_OF_KEY_TRANSLATION_TABLE_LOW_BYTE    $AC`
`   .alias FX_READ_ADDRESS_OF_KEY_TRANSLATION_TABLE_HIGH_BYTE   $AD`
`   .alias FX_READ_START_ADDRESS_OF_OS_VDU_VARIABLES_LOW_BYTE   $AE`
`   .alias FX_READ_START_ADDRESS_OF_OS_VDU_VARIABLES_HIGH_BYTE  $AF`
`   .alias FX_RW_CFS_TIMEOUT_COUNTER    $B0`
`   .alias FX_RW_INPUT_SOURCE   $B1`
`   .alias FX_RW_KEYBOARD_SEMAPHORE $B2`
`   .alias FX_RW_PRIMARY_OSHWM  $B3`
`   .alias FX_RW_CURRENT_OSHWM  $B4`
`   .alias FX_RW_RS_MODE    $B5`
`   .alias FX_READ_CHARACTER_DEFINITION_EXPLOSION_STATE $B6`
`   .alias FX_RW_CASSETTEROM_FILING_SYSTEM_SWITCH   $B7`
`   .alias FX_READ_RAM_COPY_OF_VIDEO_ULA_CONTROL_REGISTER   $B8`
`   .alias FX_READ_RAM_COPY_OF_VIDEO_ULA_PALETTE_REGISTER   $B9`
`   .alias FX_RW_ROM_NUMBER_ACTIVE_AT_LAST_BRK_ERROR    $BA`
`   .alias FX_RW_NUMBER_OF_ROM_SOCKET_CONTAINING_BASIC  $BB`
`   .alias FX_READ_CURRENT_ADC_CHANNEL  $BC`
`   .alias FX_RW_MAXIMUM_ADC_CHANNEL_NUMBER $BD`
`   .alias FX_READ_ADC_CONVERSION_TYPE  $BE`
`   .alias FX_RW_RS_USE_FLAG    $BF`
`   .alias FX_READ_RS_CONTROL_FLAG  $C0`
`   .alias FX_RW_FLASH_COUNTER  $C1`
`   .alias FX_RW_MARK_PERIOD_COUNT  $C2`
`   .alias FX_RW_SPACE_PERIOD_COUNT $C3`
`   .alias FX_RW_KEYBOARD_AUTOREPEAT_DELAY  $C4`
`   .alias FX_RW_KEYBOARD_AUTOREPEAT_PERIOD $C5`
`   .alias FX_RW_EXEC_FILE_HANDLE   $C6`
`   .alias FX_RW_SPOOL_FILE_HANDLE  $C7`
`   .alias FX_RW_ESCAPE_BREAK_EFFECT    $C8`
`   .alias FX_RW_ECONET_KEYBOARD_DISABLE    $C9`
`   .alias FX_RW_KEYBOARD_STATUS_BYTE   $CA`
`   .alias FX_RW_RS_HANDSHAKE_EXTENT    $CB`
`   .alias FX_RW_RS_INPUT_SUPPRESSION_FLAG  $CC`
`   .alias FX_RW_CASSETTERS_SELECTION_FLAG  $CD`
`   .alias FX_RW_ECONET_OS_CALL_INTERCEPTION_STATUS $CE`
`   .alias FX_RW_ECONET_OSRDCH_INTERCEPTION_STATUS  $CF`
`   .alias FX_RW_ECONET_OSWRCH_INTERCEPTION_STATUS  $D0`
`   .alias FX_RW_SPEECH_SUPPRESSION_STATUS  $D1`
`   .alias FX_RW_SOUND_SUPPRESSION_STATUS   $D2`
`   .alias FX_RW_BELL_CHANNEL   $D3`
`   .alias FX_RW_BELL_ENVELOPE_NUMBERAMPLITUDE  $D4`
`   .alias FX_RW_BELL_FREQUENCY $D5`
`   .alias FX_RW_BELL_DURATION  $D6`
`   .alias FX_RW_STARTUP_MESSAGE_AND_BOOT_OPTIONS   $D7`
`   .alias FX_RW_LENGTH_OF_SOFT_KEY_STRING  $D8`
`   .alias FX_RW_NUMBER_OF_LINES_PRINTED_SINCE_LAST_PAGE    $D9`
`   .alias FX_RW_NUMBER_OF_ITEMS_IN_VDU_QUEUE   $DA`
`   .alias FX_RW_TAB_CHARACTER_VALUE    $DB`
`   .alias FX_RW_ESCAPE_CHARACTER_VALUE $DC`
`   .alias FX_RW_CHARACTER_CO_TO_CF_STATUS  $DD`
`   .alias FX_RW_CHARACTER_DO_TO_DF_STATUS  $DE`
`   .alias FX_RW_CHARACTER_EO_TO_EF_STATUS  $DF`
`   .alias FX_RW_CHARACTER_FO_TO_FF_STATUS  $E0`
`   .alias FX_RW_FUNCTION_KEY_STATUS    $E1`
`   .alias FX_RW_SHIFT_FUNCTION_KEY_STATUS  $E2`
`   .alias FX_RW_CTRLFUNCTION_KEY_STATUS    $E3`
`   .alias FX_RW_CTRLSHIFTFUNCTION_KEY_STATUS   $E4`
`   .alias FX_RW_ESCAPE_KEY_STATUS  $E5`
`   .alias FX_RW_FLAGS_DETERMINING_ESCAPE_EFFECTS   $E6`
`   .alias FX_RW_JRQ_BIT_MASK_FOR_USER_ $E7`
`   .alias FX_RW_IRQ_BIT_MASK_FOR_  $E8`
`   .alias FX_RW_IRQ_BIT_MASK_FOR_SYSTEM_S  $E9`
`   .alias FX_READ_FLAG_INDICATING_TUBE_PRESENCE    $EA`
`   .alias FX_READ_FLAG_INDICATING_SPEECH_PROCESSOR_PRESENCE    $EB`
`   .alias FX_RW_WRITE_CHARACTER_DESTINATION_STATUS $EC`
`   .alias FX_RW_CURSOR_EDITING_STATUS  $ED`
`   .alias FX_RW_LOCATION_E_NOT_USED_BY__   $EE`
`   .alias FX_RW_LOCATION_F_NOT_USED_BY__   $EF`
`   .alias FX_RW_LOCATION__NOT_USED_BY__    $F0`
`   .alias FX_RW_LOCATION__USED_BY_FX_  $F1`
`   .alias FX_READ_RAM_COPY_OF_SERIAL_PROCESSOR_ULA $F2`
`   .alias FX_RW_TIMER_SWITCH_STATE $F3`
`   .alias FX_RW_SOFT_KEY_CONSISTENCY_FLAG  $F4`
`   .alias FX_RW_PRINTER_DESTINATION_FLAG   $F5`
`   .alias FX_RW_CHARACTER_IGNORED_BY_PRINTER   $F6`
`   .alias FX_RW_FIRST_BYTE_OF_BREAK_INTERCEPT_CODE $F7`
`   .alias FX_RW_SECOND_BYTE_OF_BREAK_INTERCEPT_CODE    $F8`
`   .alias FX_RW_THIRD_BYTE_OF_BREAK_INTERCEPT_CODE $F9`
`   .alias FX_RW_LOCATION_A_NOT_USED_BY__   $FA`
`   .alias FX_RW_LOCATION_B_NOT_USED_BY__   $FB`
`   .alias FX_RW_CURRENT_LANGUAGE_ROM_NUMBER    $FC`
`   .alias FX_RW_LAST_BREAK_TYPE    $FD`
`   .alias FX_RW_AVAILABLE_RAM  $FE`
`   .alias FX_RW_START_UP_OPTIONS   $FF`
`   .alias MuteFlag  $74`
`   .alias SoundIndex $75`
`   .alias MissFirstSound $76`
`   .alias IRQVECL $204`
`   .alias IRQVECH $205`
`   .alias osbyte $fff4`
`   .alias osword $fff1`
`   .alias oswrch $ffee`
`   ;-------------------------------------------------------------------------------`
`   ; Functionality `
`   ;-------------------------------------------------------------------------------`
`   _MAKE_SOUND:`
`       STA SoundIndex      ;//[0E9E] 85 84`
`       LDA MuteFlag        ;//[0EA0] AD 2D 2F`
`       BNE bra_0EE6        ;//[0EA3] D0 41`
`       TXA         ;//[0EA5] 8A`
`       PHA         ;//[0EA6] 48`
`       TYA         ;//[0EA7] 98`
`       PHA         ;//[0EA8] 48`
`       LDX SoundIndex      ;//[0EA9] A6 84`
`       LDA SoundSync,X     ;//[0EAB] BD 08 22`
`       STA SoundIndex      ;//[0EAE] 85 84`
`   bra_0EB0:`
`       LDA SoundSync,X     ;//[0EB0] BD 08 22`
`       STA SoundBlock1     ;//[0EB3] 8D 01 22`
`       LDA SoundChannel,X      ;//[0EB6] BD 14 22`
`       STA SoundBlock      ;//[0EB9] 8D 00 22`
`       LDY #$02        ;//[0EBC] A0 02`
`       LDA SoundVolumeEnv,X        ;//[0EBE] BD 20 22`
`       JSR _STORE_SOUND_WORD       ;//[0EC1] 20 E7 0E`
`       LDA SoundPitch,X        ;//[0EC4] BD 2C 22`
`       JSR _STORE_SOUND_WORD       ;//[0EC7] 20 E7 0E`
`       LDA SoundDuration,X     ;//[0ECA] BD 38 22`
`       JSR _STORE_SOUND_WORD       ;//[0ECD] 20 E7 0E`
`       TXA         ;//[0ED0] 8A`
`       PHA         ;//[0ED1] 48`
`       LDX #`<SoundBlock        ;//[0ED2] A2 00
        LDY #>`SoundBlock        ;//[0ED4] A0 22`
`       LDA #OSW_SOUND      ;//[0ED6] A9 07`
`       JSR osword      ;//[0ED8] 20 F1 FF`
`       PLA         ;//[0EDB] 68`
`       TAX         ;//[0EDC] AA`
`       INX         ;//[0EDD] E8`
`       DEC SoundIndex      ;//[0EDE] C6 84`
`       BPL bra_0EB0        ;//[0EE0] 10 CE`
`       PLA         ;//[0EE2] 68`
`       TAY         ;//[0EE3] A8`
`       PLA         ;//[0EE4] 68`
`       TAX         ;//[0EE5] AA`
`   bra_0EE6:`
`       RTS         ;//[0EE6] 60`
`   _STORE_SOUND_WORD:`
`       STA SoundBlock,Y        ;//[0EE7] 99 00 22`
`       INY         ;//[0EEA] C8`
`     ASL       ;//[0EEB] 0A`
`       LDA #$00        ;//[0EEC] A9 00`
`       BCC bra_0EF2        ;//[0EEE] 90 02`
`       LDA #$FF        ;//[0EF0] A9 FF`
`   bra_0EF2:`
`       STA SoundBlock,Y        ;//[0EF2] 99 00 22`
`       INY         ;//[0EF5] C8`
`       RTS         ;//[0EF6] 60`

`   SoundBlock:`
`       .byte $13       ;//[2200] .`

`   SoundBlock1:`
`       .byte $00       ;//[2201] .`
`       .byte $F1       ;//[2202] .`
`       .byte $FF       ;//[2203] .`
`       .byte $04       ;//[2204] .`
`       .byte $00       ;//[2205] .`
`       .byte $01       ;//[2206] .`
`       .byte $00       ;//[2207] .`
`   SoundSync:`
`       .byte $00       ;//[2208] .`
`       .byte $00       ;//[2209] .`
`       .byte $01       ;//[220A] .`
`       .byte $01       ;//[220B] .`
`       .byte $01       ;//[220C] .`
`       .byte $01       ;//[220D] .`
`       .byte $00       ;//[220E] .`
`       .byte $00       ;//[220F] .`
`       .byte $00       ;//[2210] .`
`       .byte $00       ;//[2211] .`
`       .byte $00       ;//[2212] .`
`       .byte $00       ;//[2213] .`
`   SoundChannel:`
`       .byte $12       ;//[2214] .`
`       .byte $13       ;//[2215] .`
`       .byte $11       ;//[2216] .`
`       .byte $10       ;//[2217] .`
`       .byte $11       ;//[2218] .`
`       .byte $10       ;//[2219] .`
`       .byte $12       ;//[221A] .`
`       .byte $13       ;//[221B] .`
`       .byte $13       ;//[221C] .`
`       .byte $13       ;//[221D] .`
`       .byte $13       ;//[221E] .`
`       .byte $13       ;//[221F] .`
`   SoundVolumeEnv:`
`       .byte $01       ;//[2220] .`
`       .byte $F1       ;//[2221] .`
`       .byte $02       ;//[2222] .`
`       .byte $03       ;//[2223] .`
`       .byte $02       ;//[2224] .`
`       .byte $F1       ;//[2225] .`
`       .byte $01       ;//[2226] .`
`       .byte $04       ;//[2227] .`
`       .byte $00       ;//[2228] .`
`       .byte $F1       ;//[2229] .`
`       .byte $F1       ;//[222A] .`
`       .byte $04       ;//[222B] .`
`   SoundPitch:`
`       .byte $64       ;//[222C] d`
`       .byte $C8       ;//[222D] .`
`       .byte $50       ;//[222E] P`
`       .byte $07       ;//[222F] .`
`       .byte $50       ;//[2230] P`
`       .byte $07       ;//[2231] .`
`       .byte $AA       ;//[2232] .`
`       .byte $78       ;//[2233] x`
`       .byte $00       ;//[2234] .`
`       .byte $00       ;//[2235] .`
`       .byte $04       ;//[2236] .`
`       .byte $96       ;//[2237] .`
`   SoundDuration:`
`       .byte $0A       ;//[2238] .`
`       .byte $02       ;//[2239] .`
`       .byte $FF       ;//[223A] .`
`       .byte $0A       ;//[223B] .`
`       .byte $FF       ;//[223C] .`
`       .byte $04       ;//[223D] .`
`       .byte $0A       ;//[223E] .`
`       .byte $FF       ;//[223F] .`
`       .byte $01       ;//[2240] .`
`       .byte $01       ;//[2241] .`
`       .byte $01       ;//[2242] .`
`       .byte $FF       ;//[2243] .`
` `
`   Env1:`
`       .byte $01,$02,$ff,$fe,$ff,$0a,$0a,$32,$7e,$fc,$fc,$fc,$7e,$00`
`   Env2:`
`       .byte $02,$02,$04,$00,$FC,$0A,$0A,$0A,$01,$00,$00,$00,$01,$01`
`   Env3:`
`           .byte $03,$04,$00,$00,$00,$01,$01,$01,$7e,$fc,$ff,$fc,$7e,$50`
`   Env4:`
`       .byte $04,$01,$08,$04,$f4,$04,$04,$04,$64,$00,$00,$00,$64,$64`
`   _INITSOUND:`
`       LDA #VDU_MODE       ;//[2FF0] A9 16`
`       JSR oswrch      ;//[2FF2] 20 EE FF`
`       LDA #VDU_ENABLE_PRINTER     ;//[2FF5] A9 02`
`       JSR oswrch      ;//[2FF7] 20 EE FF`
`       LDA #0`
`       STA     MuteFlag`

`       LDX #`<Env1      ;//[0ED2] A2 00
        LDY #>`Env1      ;//[0ED4] A0 22`
`       LDA #OSW_DEFINE_ENVELOPE ;//[0ED6] A9 07`
`       JSR osword      ;//[0ED8] 20 F1 FF`
`       `
`       LDX #`<Env2      ;//[0ED2] A2 00
        LDY #>`Env2      ;//[0ED4] A0 22`
`       LDA #OSW_DEFINE_ENVELOPE ;//[0ED6] A9 07`
`       JSR osword      ;//[0ED8] 20 F1 FF`
`       LDX #`<Env3      ;//[0ED2] A2 00
        LDY #>`Env3      ;//[0ED4] A0 22`
`       LDA #OSW_DEFINE_ENVELOPE ;//[0ED6] A9 07`
`       JSR osword      ;//[0ED8] 20 F1 FF`
`       LDX #`<Env4      ;//[0ED2] A2 00
        LDY #>`Env4      ;//[0ED4] A0 22`
`       LDA #OSW_DEFINE_ENVELOPE ;//[0ED6] A9 07`
`       JSR osword      ;//[0ED8] 20 F1 FF`
`       RTS`
