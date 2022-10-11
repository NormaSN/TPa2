.model small
.stack
.data
     
     Saludo DB "Hola profe","$"
     Solicitud1 DB "Por favor, ingrese un texto", "$"
     Solicitud2 DB "Por favor, vuelva a ingresar el texto", "$"
     
     Saltolinea DB 0Ah, 0Dh, "$"       
     
     Textooriginal DB 101, 0, 101 dup("$"), "$"
     Textorepetido DB 101, 0, 101 dup("$"), "$"
     

.code
   
   
    Inicio:
    
    mov ax, @data                   ; Estas dos lineas permiten que se  reconozcan las variables declaradas
    mov ds, ax
    
    mov ax, 0                       ; Inicializo los registros en 0
    mov bx, 0
    mov cx, 0
    mov dx, 0
         
        ; Muestra "Hola profe" por pantalla
    mov ah, 09h                     ; Mostrar string por pantalla
    mov dx, offset Saludo           ; Cargo en DX la direccion de memoria de Saludo
    int 21h
    
    call Saltodelinea
        
        ; Muestra "Por favor, ingrese un texto" por pantalla       
    mov ah, 09h                     ; Mostrar string por pantalla
    mov dx, offset Solicitud1       ; Cargo en DX la direccion de memoria de Salicitud1
    int 21h
    
    call Saltodelinea
             
        ; Leer el texto por pantalla 
    mov ah, 0Ah                     ; Leer string por pantalla                        
    mov dx, offset Textooriginal    ; Cargar el string en DX
    int 21h
    
    call Saltodelinea
    
        ; Muestra "Por favor, vuelva a ingresar el texto" por pantalla
    mov ah, 09h                     ; Mostrar string por pantalla
    mov dx, offset Solicitud2       ; Cargo en DX la direccion de memoria de Solicitud2
    int 21h
    
    call Saltodelinea
    
        ; Leer el segundo texto por pantalla
    mov ah, 0Ah                     ; Leer segundo string por pantalla
    mov dx, offset Textorepetido    ; Cargar el string en DX        
    int 21h
    
        ; Comparar caracter a caracter los dos textos
    mov si, 0                       ; Inicializo SI en 0 ¨o lo debiera inicializar en 2?
    mov cx, 101                     ; Inicializo el contador en 101 porque son los elementos que tengo que comparar
    
    Comparar:
    
    cmp si, 101                     ; SI compara con 101
    je Fin                          ; Si SI=101, salta
    
    
    mov bl, Textorepetido[si]       ; Traigo el caracter del segundo texto
    cmp bl, Textooriginal[si]       ; Comparo con el caracter original
    jne Caracterequivocado          ; Si no es igual, salta a Caracterequivocado
    
    inc si                          ; Si es igual, incrementa SI
    loop Comparar                   ; Vuelve a Comparar
           
    jmp Fin                         ; Va al procedimiento de Fin    
        
        
mov ax, 4C00h
Int 21h

   
Saltodelinea proc
    mov ah, 09h
    mov dx, offset Saltolinea
    int 21h
    ret
Saltodelinea endp




Caracterequivocado proc
       
    
Caracterequivocado endp    



Fin proc

    
Fin endp    




     
   
    End Inicio    
      
        
    
    

