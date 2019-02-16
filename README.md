# Divertirsi con il tuo Commodore 64

## Introduzione

* **Versione Assembler** per compilare ed eseguire la versione assembler e' necessario un ambiente di sviluppo; i programmi proposti in questo libro sono stati progettati utilizando CBM Studio come IDE e VICE come emulatore (entrambi disponibili per diversi sitemi operativi). 

* **Versione Basic** la versione BASIC del programma può essere inserita (con molta pazienza) ed eseguita direttamente su un C64 reale senza la necessità di strumenti esterni.

Una volta ottenuto il programma compilato in formato PRG (sia partendo da un listato BASCI che Assembler) questo può essere eseguito su un C64 reale. Si consiglia una ricerca sul web per trovare la procedura più facile per voi.

## Screen Player

Giocare con lo schermo: questo programma ripulisce il contenuto dello schermo e cambia i colori di bordo e sfondo.

![Screen Player](screen-player.png)

### Versione Assembler

```asm
; Screen Player
; clear screen content and play with border and
; background colors

; daniele.olmisani@gmail.com


; jump location of BASIC RUN command
*=$0801

; 10 SYS (2064)

        BYTE    $0E, $08, $0A, $00, $9E, $20, $28, $32
        BYTE    $30, $36, $34, $29, $00, $00, $00

; start of program at $0810

;       jsr $E544   ; clear screen kernal routine

; otherwise implemet a clear loop

        lda #$20    ; space screen code
        ldx #$FA    ; starting counter

clear   sta $0400,x ; clear screen memory
        sta $04FA,x ; 250 bytes at a time
        sta $05F4,x
        sta $06EE,x

        dex         ; decrement X
  
        bne clear   ; loop until X turn zero

BORDER = $D020
SCREEN = $D021

start   inc SCREEN  ; increase screen colour 
        inc BORDER  ; increase border colour
        jmp start   ; repeat
```

### Versione Basic
Questa versione del programma può essere inserita ed eseguita direttamente sul C64.

```
100 REM SCREEN PLAYER
110 SA = 3072
120 FOR N = 0 TO 27
130 READ A% : POKE SA+N,A%: NEXT N
140 SYS SA
150 END 
160 DATA 169,32,162,0,157,0,4,157
170 DATA 0,5,157,0,6,157,232,6
180 DATA 232,208,241,238,33,208,238,32
190 DATA 208,76,19,12
```
