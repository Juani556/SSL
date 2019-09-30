Usuario Github: Juani556  
Legajo: 160.767-4  
Apellido: Iglesias  
Nombre: Juan Ignacio  
  
## 01 - Fases de la Traducción y Errores  
  
####  Consignas  
  
1. Escribir hello2.c, que es una  variante del hello.c:
    ``` [C]
    #include <stdio.h>

    int/*medio*/main(void){ 
     int i=42;
     prontf("La respuesta es %d\n");
    ```
2. Preprocesar hello2.c, no compilar, y generar hello2.i. Analizar su contenido.
3. Escribir hello3.c, una nueva variante:
    ``` [C]
    int printf(const char *s, ...);

    int main(void){
     int i=42;   
     prontf("La respuesta es %d\n");
    ```
4. Investigar la semántica de la primera línea.
5. Preprocesar hello3.c, no compilar, y generar hello3.i. Buscar diferencias entre hello3.c y hello3.i.
6. Compilar el resultado y generar hello3.s, no ensamblar.
7. Corregir en el nuevo archivo hello4.c y empezar de nuevo, generar hello4.s, no ensamblar.
8. Investigar hello4.s
9. Ensamblar hello4.s en hello4.o, no vincular.
10. Vincular hello4.o con la biblioteca estándar y generar el ejecutable.
11. Corregir en hello5.c y generar el ejecutable.
12. Ejecutar y analizar el resultado.
13. Corregir en hello6.c y empezar de nuevo.
14. Escribir hello7.c, una nueva variante:
    ```[C]
    int main(void){
     int i=42;    
        printf("La respuesta es %d\n", i);
     }
     ```
15. Explicar porqué funciona.  
  
### Resolución  

2- Comando:  

    gcc -E hello2.c -o hello2.i 
Nos queda el archivo hello2.i que paso por el preprocesador, el cual reemplazo los comentarios por un espacio entre el int y el main. Ademas reemplazo la linea de include por el contenido del archivo stdio.h.  
  
4- La semántica de la primera línea es la declaracion de una función llamada printf que recibe un puntero a char y una cantidad indeterminada de otros argumentos.  
  
5-Comando:  
  
    gcc -E  hello3.c -o hello3.i  
En lo que al código específico se refiere no hay ninguna diferencia. Lo único que en el hello3.i se agregan unas anotaciones al principio del archivo.  
  
6-Comando:  
  
    gcc -S hello3.i -o hello3.s  
Esto produce una advertencia del compilador en el que sugiere si en la llamada a prontf en realidad no quisimos llamar a printf que esta declarada al principio del archivo. Produce también error porque falta el corchete de cierre del main. Este es un error de sintaxis.  
  
7- Comandos:  
  
    gcc -E  hello4.c -o hello4.i
    gcc -S hello4.i -o hello4.s  
Ya no mostró errores, pero sigue la advertencia del prontf.
  
8- El archivo hello4.s contiene el programa codificado en lenguaje assembler.  
  
9- Comando:  
  
    gcc -c hello4.s -o hello4.o    

10-Comando:  
  
    gcc hello4.o -o hello4.exe  
No pudo realizar la vinculación, porque nos dice que hay una referencia indefinida a prontf 
  
11-Comando:  
  
    gcc hello5.c -o hello5.exe  
  
12-Comando:  
  
    hello5.exe  
Resultado:  
  
    La respuesta es 4200640  
No es la salida esperada.  
  
13-Comandos:  
  
    gcc hello6.c -o hello6.exe
    hello6.exe  
Resultado:  
  
    La respuesta es 42  

14-Comandos:  
  
    gcc hello7.c -o hello7.exe
    hello7.exe  
Nos advierte que falta la declaracion de printf y nos dice que la explicitemos o que incluyamos el archivo stdio.h.  
  
Resultado:  
  
    La respuesta es 42  
  
15- Funciona porque la llamada a printf en el código cuenta como una declaración implícita. Y además al estar printf en la librería estándar no hay problema para vincularla luego.  
  



