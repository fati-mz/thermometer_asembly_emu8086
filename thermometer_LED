#start=thermometer.exe# 
#start=led_display.exe#
#make_bin#

name "thermo"  
    
    
; define temperature range in Fahrenheit and Celsius
;low_temp db 5
;high_temp db 40
celsius_low_temp db 0
celsius_high_temp db 0


; convert Fahrenheit to Celsius and store the result in the corresponding Celsius temperature variables
mov al, 5
sbb al, 32
mov bl, 5
imul bl
mov bl, 9
idiv bl
mov [celsius_low_temp], al

mov al, 40
sbb al, 32
mov bl, 5
imul bl
mov bl, 9
idiv bl
mov [celsius_high_temp], al

; set data segment to code segment:
mov ax, cs
mov ds, ax



start:

    in al, 125 
     
    ;show in LED           
    cmp al,0
    jl ng
    sub ax,256           
    out 199,ax 
    add ax,256
    jmp ignore_ng
    ng:
    sbb ax,512           
    out 199,ax 
    add ax,512 
    ignore_ng:
    
    ; check if temperature is below low_temp and turn on the heater if it is
    cmp al, [celsius_low_temp]
    jl  low

    ; check if temperature is above high_temp and turn off the heater if it is
    cmp al, [celsius_high_temp]  
    jle  ok
    jg  high

low:
    mov al, 1
    out 127, al   ; turn heater "on".
    jmp ok

high:
    mov al, 0
    out 127, al   ; turn heater "off". 

ok:
    jmp start   ; endless loop.
