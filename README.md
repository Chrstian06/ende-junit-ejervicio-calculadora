# Testing con Junit

Este es un ejemplo sencillo de pruebas unitarias usando Junit 5

Observa que este proyecto no tiene ninguna clase con el método `main`, no nos hace fatal. Además, tampoco tiene ningún `scanner` ni ningún `print`.

Haz un fork de este proyecto en tu repositorio de Github y contesta a las siguientes preguntas:

1. ¿Qué sentido puede tener este proyecto y para que lo podrías usar?

Este proyecto es una calculadora básica que otros programas pueden usar. No tiene main porque no es un programa que se ejecute solo; es una librería de funciones matemáticas.

2. Revisa las pruebas de la suma y comenta lo que te parezca de interés

Lo más destacable:

    Tiene una prueba que falla a propósito (sumarPositivosMal) para enseñar cómo JUnit marca los errores cuando el resultado no es el esperado.

    Usa assertAll para probar varias sumas en un solo test (positivos, negativos, con cero). Si algo falla, te dice exactamente qué caso fue.

    Incluye mensajes descriptivos como "1 + 4 = 5" para identificar rápidamente dónde está el fallo.

3. Realiza un estudio de caja negra de la división e implementa las pruebas en junit: Se realizará en markdown.

### Particiones de equivalencia identificadas:

| Caso                        | Entradas (a, b) | Salida esperada | Tipo de prueba |
| ----------------------------| -----------------| -----------------| -------------|
| División positiva           | 10 / 2          | 5               | Válida         |
| Positivo entre negativo     | 10 / -2         | -5              | Válida         |
| Negativo entre negativo     | -10 / -2        | 5               | Válida         |
| Cero dividido               | 0 / 5           | 0               | Válida         |
| Dividendo menor que divisor | 3 / 5           | 0               | Válida         |
| División con resto          | 7 / 2           | 3               | Válida         |
| División por cero           | 10 / 0          | Lanza excepción | No válida      |
| Cero entre cero             | 0 / 0           | Lanza excepción | No válida      |

### Implementación en JUnit (añadir a CalculadoraTest.java):

```java
@Test
@DisplayName("Probar divisiones válidas")
void divisionesValidas() {
    assertAll("Divisiones correctas",
        () -> assertEquals(5, Calculadora.dividir(10, 2), "10/2 = 5"),
        () -> assertEquals(-5, Calculadora.dividir(10, -2), "10/-2 = -5"),
        () -> assertEquals(5, Calculadora.dividir(-10, -2), "-10/-2 = 5"),
        () -> assertEquals(0, Calculadora.dividir(0, 5), "0/5 = 0"),
        () -> assertEquals(0, Calculadora.dividir(3, 5), "3/5 = 0"),
        () -> assertEquals(3, Calculadora.dividir(7, 2), "7/2 = 3")
    );
}

@Test
@DisplayName("Probar divisiones no válidas (por cero)")
void divisionesNoValidas() {
    assertAll("Divisiones que lanzan excepción",
        () -> assertThrows(OperacionNoValidaException.class, 
            () -> Calculadora.dividir(10, 0), "10/0 debe lanzar excepción"),
        () -> assertThrows(OperacionNoValidaException.class, 
            () -> Calculadora.dividir(-5, 0), "-5/0 debe lanzar excepción"),
        () -> assertThrows(OperacionNoValidaException.class, 
            () -> Calculadora.dividir(0, 0), "0/0 debe lanzar excepción")
    );
}



## Instrucciones

El alumno deberá hacer un fork de este proyecto e implementar la solución solicitada (preguntas y código).

>Se deberá utilizar este fichero, y los artefactos de código del proyecto, para resolver el ejercicio.


**Si no se puede acceder al repositorio la evaluación del ejercicio será de 0. No se evaluarán entregas modificadas/entregadas fuera del plazo establecido en la tarea**
