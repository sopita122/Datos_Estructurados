# Actividad 5 - Modelado de datos con Struct y Punteros

**Materia**: Laboratorio de Programación
**Curso**: 5° 3°
**Año**: 2026
**Lenguaje**: C++

## 1.Objetivo del manual
El objetivo de este manual es explicar cómo está desarrollado el programa de la Actividad 5 y cómo se utilizan las estructuras (struct) y los punteros en C++.
El programa permite modelar una entidad mediante una estructura llamada EntidadProyecto, ingresar sus datos mediante una función y acceder a ellos utilizando un puntero y el operador flecha (->).
También se explica el uso de cin.ignore() y cin.getline() para ingresar correctamente datos de texto.

## 2.¿Qué es un struct?
Un struct permite agrupar diferentes variables relacionadas dentro de una misma estructura lógica.
En nuestro programa se utiliza:

struct EntidadProyecto {
    int id;
    char nombre[50];
    float metrica;
};

La estructura contiene tres datos:
<pre>
    `id`: identificador de la entidad.
    `nombre`: nombre o descripción de la entidad.
    `metrica`: valor decimal relacionado con la entidad.
</pre>
De esta manera, en lugar de trabajar con varias variables separadas, los datos quedan agrupados dentro de EntidadProyecto. 

## 3.Creación de la entidad
En la función main() se crea una variable de tipo EntidadProyecto:
<pre>
    `EntidadProyecto miEntidad` = {0, "Vacio - [Su Nombre y Apellido]", 0.0f};
</pre>
La variable comienza con valores iniciales y posteriormente sus datos son modificados mediante la función cargarDatos().
La estructura se crea una sola vez en main() y se utiliza durante la ejecución del programa.

## 4.Puntero a un struct
Un puntero almacena una dirección de memoria.
En nuestro programa se obtiene la dirección de miEntidad utilizando el operador &:
<pre>
    `cargarDatos(&miEntidad);`
</pre>
El operador & permite obtener la dirección de memoria de la variable.
La función recibe esa dirección mediante un puntero:
<pre>
    `void cargarDatos(EntidadProyecto* ptr);`
</pre>
Por lo tanto, ptr contiene la dirección de miEntidad. 

## 5.Operador flecha ->
Cuando tenemos un puntero hacia una estructura, utilizamos el operador flecha (->) para acceder a sus miembros.
En nuestro programa se utiliza:
<pre>
    `ptr->id`
    `ptr->nombre`
    `ptr->metrica`
</pre>
Por ejemplo:
<pre>
    `cin >> ptr->id;`
</pre>
Esto permite modificar el miembro id de la estructura original.
La diferencia entre ambas formas es:

| Situación | Forma de acceso |
|---|---|
| Variable de tipo `EntidadProyecto` | `miEntidad.id` |
| Puntero a `EntidadProyecto` | `ptr->id` |
El operador -> se utiliza porque ptr es un puntero y no una variable directa de tipo EntidadProyecto.

## 6.Pasaje de la dirección mediante puntero

La función cargarDatos() recibe un puntero:
<pre>
    `void cargarDatos(EntidadProyecto* ptr)`
</pre>
Desde main() se le envía la dirección:
<pre>
    `cargarDatos(&miEntidad);`
</pre>
Esto permite que la función trabaje directamente sobre la estructura original.
Por ejemplo:
<pre>
    `ptr->id = 10;`
</pre>
modifica el id de miEntidad.
De esta forma no es necesario crear otra estructura para realizar los cambios. 

## 7.Carga de datos
La función encargada de ingresar los datos es cargarDatos():
<>
    void cargarDatos(EntidadProyecto* ptr) {
        cout << "\n--- INGRESO DE DATOS MEDIANTE OPERADOR FLECHA ---" << endl;

        cout << "=> Ingrese el ID de la entidad (entero): ";
        cin >> ptr->id;

        cin.ignore();

        cout << "=> Ingrese el Nombre o Descripcion: ";
        cin.getline(ptr->nombre, 50);

        cout << "=> Ingrese la Metrica de Operacion (decimal/float): ";
        cin >> ptr->metrica;
    }
</>
La función solicita tres datos al usuario:
<pre>
    - `ID.`
    - `Nombre o descripción.`
    - `Métrica de operación.`
</pre>
Cada dato se almacena directamente dentro de la estructura. 

## 8.Buffer de entrada: cin.ignore() y cin.getline()
Después de utilizar:
<pre>
    `cin >> ptr->id;`
</pre>
queda el salto de línea producido por la tecla Enter dentro del buffer de entrada.
Por eso se utiliza:
<pre>
    `cin.ignore();`
</pre>    
antes de:
<pre>
    `cin.getline(ptr->nombre, 50);`
</pre>
Esto permite que getline() pueda leer correctamente el nombre completo.
Por ejemplo:
<pre>
    `Producto Cooperadora`
</pre>
se puede ingresar completo, incluyendo el espacio.
Si se omitiera cin.ignore(), getline() podría encontrar el salto de línea pendiente y no permitir ingresar correctamente el nombre.

## 9.Funcionamiento de main()
La función main() realiza las operaciones principales del programa.
Primero crea la estructura:
<pre>
    `EntidadProyecto miEntidad = {0, "Vacio - [Su Nombre y Apellido]", 0.0f};`
</pre>
Después llama a:
<pre>
    `cargarDatos(&miEntidad);`
</pre>
Una vez que la función termina, main() muestra los datos almacenados:
<pre>
    `cout << "ID Registrado:     " << miEntidad.id << endl;`
    `cout << "Nombre Registrado: " << miEntidad.nombre << endl;`
    `cout << "Metrica Guardada:  " << miEntidad.metrica << endl;`
</pre>
Finalmente muestra la dirección de memoria:
<pre>
    `cout << "Direccion RAM Hexadecimal: " << &miEntidad << endl;` 
</pre>

## 10.Dirección de memoria
El programa permite observar la dirección de memoria donde se encuentra almacenada miEntidad.
Se obtiene mediante:
<pre>
    `&miEntidad`
</pre>
La dirección puede aparecer, por ejemplo, de esta forma:
<pre>
    `0x7ffd1234abcd`
</pre>
El valor exacto puede cambiar cada vez que se ejecuta el programa, ya que depende de la ubicación que el sistema operativo asigna en la memoria RAM.

## 11.Errores comunes
Durante el desarrollo se deben tener en cuenta algunos errores frecuentes:
# 1.Utilizar . con un puntero
<pre>
Incorrecto:
    ptr.id
Correcto:
    ptr->id
</pre>

# 2.Olvidar cin.ignore()
Si se utiliza cin >> antes de getline(), es necesario limpiar el buffer para evitar problemas al ingresar texto.

# 3.Confundir & y * 
El operador & permite obtener una dirección de memoria:
<pre>
    &miEntidad
</pre>
Mientras que * se utiliza en la declaración para indicar que una variable es un puntero:
<pre>
EntidadProyecto* ptr;
</pre>

# 4.Modificar la estructura incorrectamente
Si se agrega un nuevo miembro al struct, también se debe agregar su carga y, si corresponde, su visualización en el programa. 

## 12.Conclusion
El programa desarrollado permite aplicar los conceptos de struct, punteros, operador flecha (->) y manejo del buffer de entrada en C++.
La estructura permite agrupar datos relacionados dentro de una misma entidad, mientras que el puntero permite trabajar con la dirección de memoria de esa estructura y modificar sus datos desde una función.