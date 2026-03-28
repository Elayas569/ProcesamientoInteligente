# Cómputo Evolutivo — Reporte de Lectura y Clases Base

> **Referencia:** Kuri, Á. (2002). _Algoritmos genéticos_. México D.F.: Instituto Politécnico Nacional.  
> Temas leídos: 1.1 La naturaleza como optimizadora · 1.2 Un poco de biología

---

## Reporte de Lectura

### 1.1 La naturaleza como optimizadora

La naturaleza lleva millones de años resolviendo problemas extremadamente complejos sin ningún diseñador explícito. La evolución biológica es, en esencia, un proceso de búsqueda y optimización: ante un entorno cambiante, los organismos que mejor se adaptan sobreviven y se reproducen, transmitiendo sus características a la siguiente generación. Con el tiempo, la población en su conjunto se "mueve" hacia soluciones cada vez mejores.

Kuri destaca que este proceso tiene tres propiedades que lo hacen atractivo para la computación:

- **Es paralelo:** muchos individuos exploran el espacio de soluciones al mismo tiempo.
- **Es robusto:** no se queda atrapado fácilmente en mínimos locales porque mantiene diversidad en la población.
- **Es general:** no necesita conocer la estructura matemática del problema; solo requiere poder evaluar qué tan buena es una solución.

Estas propiedades inspiraron el desarrollo de los **Algoritmos Genéticos (AG)**, que imitan el proceso evolutivo para encontrar soluciones óptimas o cercanas al óptimo en problemas donde los métodos clásicos fallan o son demasiado costosos.

La idea central es simple: si la naturaleza puede "diseñar" ojos, alas o sistemas inmunes mediante selección y herencia, un algoritmo que replique ese mecanismo debería ser capaz de encontrar buenas soluciones a problemas de ingeniería, diseño o búsqueda.

---

### 1.2 Un poco de biología

Para entender los AG es necesario comprender los conceptos biológicos que los fundamentan. Kuri los resume de la siguiente manera:

**Genotipo y fenotipo**  
Cada organismo posee un **genotipo**: la información genética codificada en sus cromosomas (cadenas de ADN compuestas por genes). El **fenotipo** es la expresión observable de ese genotipo, es decir, las características físicas y funcionales del organismo. En los AG, el genotipo es el cromosoma codificado (generalmente en binario) y el fenotipo es la solución que ese cromosoma representa.

**Cromosoma y genes**  
Un cromosoma es una estructura que contiene unidades de información llamadas **genes**. Cada gen ocupa una posición fija en el cromosoma (locus) y puede tomar distintos valores (alelos). La combinación de todos los genes define al individuo.

**Selección natural**  
La presión del entorno actúa como filtro: los individuos con mayor **aptitud** (_fitness_) — es decir, los que mejor resuelven el problema de supervivencia — tienen mayor probabilidad de reproducirse. Este principio darwiniano se traduce en los AG como una función objetivo que asigna un valor numérico a cada solución.

**Reproducción y cruzamiento**  
Cuando dos individuos se reproducen, sus cromosomas se combinan mediante el **cruzamiento** (_crossover_): se toma una parte del cromosoma de cada progenitor para formar un nuevo individuo. Esto permite heredar características útiles de ambos padres.

**Mutación**  
Ocasionalmente ocurren errores en la copia del ADN que modifican uno o más genes de forma aleatoria. La **mutación** introduce variedad genética y evita que la población converja prematuramente hacia una solución subóptima. En los AG se aplica con una tasa baja para no destruir soluciones ya buenas.

**Generaciones**  
El ciclo evolutivo completo — evaluación, selección, cruzamiento y mutación — constituye una **generación**. A lo largo de múltiples generaciones, la aptitud promedio de la población tiende a aumentar.

---

## Diagrama UML de las Clases

```mermaid
classDiagram
    class Individuo {
        +int longitud
        +list~int~ cromosoma
        +float aptitud
        +__init__(longitud, cromosoma)
        -_generar_cromosoma() list
        +evaluar(funcion_objetivo) float
        +mutar(tasa_mutacion) None
        +fenotipo() int
        +__repr__() str
    }

    class Poblacion {
        +int tamanio
        +int longitud_cromosoma
        +list~Individuo~ individuos
        +int generacion
        +Individuo mejor
        +__init__(tamanio, longitud_cromosoma)
        -_seleccion_ruleta() Individuo
        -_cruzar(padre, madre) tuple
        +evaluar_poblacion(funcion_objetivo) None
        +evolucionar(funcion_objetivo, tasa_mutacion) None
        +estadisticas() dict
        +__repr__() str
    }

    Poblacion "1" *-- "N" Individuo : contiene
    Poblacion ..> Individuo : crea en cruzamiento
```
