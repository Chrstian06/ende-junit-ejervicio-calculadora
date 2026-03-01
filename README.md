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

##### Implementación en junit:
```java
@Test
    void dividirPositivos() {
        int valor1 = 4;
        int valor2 = 2;
        int esperado = 2;

        assertEquals(esperado, Calculadora.dividir(valor1, valor2));
    }

    @Test
    void dividirNegativos() {
        int valor1 = -6;
        int valor2 = -3;
        int esperado = 2;

        assertEquals(esperado, Calculadora.dividir(valor1, valor2));
    }

    @Test
    void dividirPositivoNegativo() {
        int valor1 = 4;
        int valor2 = -4;
        int esperado = -1;

        assertEquals(esperado, Calculadora.dividir(valor1, valor2));
    }

    @Test
    void dividirNegativoPositivo() {
        int valor1 = -8;
        int valor2 = 4;
        int esperado = -2;

        assertEquals(esperado, Calculadora.dividir(valor1, valor2));
    }

    @Test
    void dividirCeroEntrePositivo() {
        int valor1 = 0;
        int valor2 = 4;
        int esperado = 0;

        assertEquals(esperado, Calculadora.dividir(valor1, valor2));
    }

    @Test
    void dividirCeroEntreNegativo() {
        int valor1 = 0;
        int valor2 = -2;
        int esperado = 0;

        assertEquals(esperado, Calculadora.dividir(valor1, valor2));
    }
    
    @Test
    void dividirEntreCero() {
        int valor1 = 7;
        int valor2 = 0;

        assertThrows(OperacionNoValidaException.class, () -> {
         Calculadora.dividir(valor1, valor2);
      });
    }

    @Test
    void dividirNegativoEntreCero() {
        int valor1 = -3;
        int valor2 = 0;

        assertThrows(OperacionNoValidaException.class, () -> {
         Calculadora.dividir(valor1, valor2);
      });
    }

    @Test
    void dividirCeroEntreCero() {
        int valor1 = 0;
        int valor2 = 0;

        assertThrows(OperacionNoValidaException.class, () -> {
         Calculadora.dividir(valor1, valor2);
      });
    }
```
**Si no se puede acceder al repositorio la evaluación del ejercicio será de 0. No se evaluarán entregas modificadas/entregadas fuera del plazo establecido en la tarea**
