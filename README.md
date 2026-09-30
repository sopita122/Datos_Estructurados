# Actividad 5 - Modelado de datos con `struct` y punteros

**Materia:** Laboratorio de Programación (LPR), 5.º año  
**Curso/división:** 5.º 3.ª A-B  
**Integrantes:** Sofia Salaberry, Thiago Goya y Martina Araujo  


## Introduccion
Esta actividad corresponde a la materia Laboratorio de Programación y tiene como objetivo trabajar con el modelado de datos utilizando estructuras (struct) y punteros en C++.

## Objetivo de la actividad
Los objetivos principales de esta actividad son:
    - Crear y utilizar una estructura (struct) en C++.
    - Agrupar diferentes tipos de datos dentro de una misma entidad.
    - Utilizar punteros para acceder a una estructura mediante su dirección de memoria.
    - Comprender el funcionamiento del operador flecha (->).
    - Pasar una estructura a una función mediante un puntero.
    - Utilizar cin.ignore() para limpiar el buffer de entrada.
    - Utilizar cin.getline() para ingresar textos completos.
    - Observar la dirección de memoria de una estructura.

## Estructura 
Para realizar la actividad se creó la estructura EntidadProyecto:
    struct EntidadProyecto {
        int id;
        char nombre[50];
        float metrica;
    };
La estructura contiene tres miembros:
    `id`: almacena el identificador de la entidad.
    `nombre`: almacena el nombre o descripción.
    `metrica`: almacena un valor decimal relacionado con la entidad.

El uso de struct permite mantener estos datos agrupados en una misma entidad en lugar de trabajar con variables separadas.

## Uso de Punteros 
La función encargada de cargar los datos recibe un puntero:
    `void cargarDatos(EntidadProyecto* ptr);`
Desde la función main() se envía la dirección de la estructura mediante:
    `cargarDatos(&miEntidad);`
El operador & permite obtener la dirección de memoria de miEntidad.
Como la función recibe un puntero, se utiliza el operador flecha (->) para acceder a los miembros de la estructura:
    `ptr->id`
    `ptr->nombre`
    `ptr->metrica`
Esto permite modificar directamente los datos de la estructura original.

## Uso de cin.ignore() y cin.getline()
Después de ingresar el ID utilizando cin >>, queda un salto de línea en el buffer de entrada. Por este motivo se utiliza:
    `cin.ignore();`
Luego se utiliza:
    `cin.getline(ptr->nombre, 50);`
Esto permite ingresar el nombre o descripción completa, incluyendo espacios.

## Funcionamiento del programa
El programa comienza creando una variable de tipo EntidadProyecto y asignándole valores iniciales.
Después se llama a la función cargarDatos() enviando la dirección de memoria de la estructura. La función solicita al usuario el ID, el nombre o descripción y la métrica.
Una vez ingresados los datos, el programa vuelve a main() y muestra la información almacenada. También muestra la dirección de memoria de la estructura en formato hexadecimal.
El funcionamiento general puede resumirse de la siguiente manera:
<pre>
Inicio
  ↓
Crear EntidadProyecto
  ↓
Inicializar sus datos
  ↓
Enviar su dirección a cargarDatos()
  ↓
Ingresar ID
  ↓
Ingresar nombre o descripción
  ↓
Ingresar métrica
  ↓
Mostrar los datos registrados
  ↓
Mostrar dirección de memoria
  ↓
Fin
</pre>

## Estructura del repositorio 
<pre>
datos con estructura/
├── .gitignore 
├── LICENSE 
├── README.md 
├── docs/ 
│   ├── InformeEEST1_LPR2026_ACT05.pdf 
│   │ 
│   └── manuales/ 
│       ├──manual_programador_v1.0.0.pdf
│       └── manual_programador_v1.0.0.md 
│ 
├── src/ 
│ └── main.cpp 
│
└── capturas/ 
    └── ejecucion_struct.png
</pre>



















