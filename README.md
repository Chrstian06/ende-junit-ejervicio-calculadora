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

- En este caso tenemos dos entradas (dividendo y dividor) y una salida que es el resultado de la division.
- Determinar clases equivalentes:
   - Dividendo: todos los números son válidos.
   - Divisor: todos los números son válidos menos el 0; el 0 no es válido.
- Valores límites: (cada entrada tiene unos valores limites distintos)
   - Dividendo (D1): 
      - -infinito: valor mínimo.
      - +infinito: valor máximo.
      - Válidas: D1 < 0 | D1 > 0 | D1 = 0
   - Divisor (D2):
      - -infinito: valor mínimo.
      - 0: valor intermedio pero no valido
      - +infinito: valor máximo.
      - Válidas: D2 < 0 | D2 > 0
      - No Válidas: D2 = 0 
   - Conjetura de errores: comprobaremos que cuando el divisor sea 0 dará error.
- Casos de pruebas: (aplicando los limites para cubrir todos los casos)
    | Caso de Prueba | Dividendo | Divisor | Salida |
    | - | - | - | - |
    | CP1 | 4 | 2 | 2 |
    | CP2 | -6 | -3 | 2 |
    | CP3 | 4 | -4 | -1 |
    | CP4 | -8 | 4 | -2 |
    | CP5 | 0 | 4 | 0 |
    | CP6 | 0 | -2 | 0 |
    | CP7 | 7 | 0 | ERROR |
    | CP8 | -3 | 0 | ERROR |
    | CP9 | 0 | 0 | ERROR |


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
