<h1 style="color:blue"> FUNCIONES Y CLASES PHP - GUÍA DE ESTUDIO</h1>

<h2>Guía algunas de Funciones  y Clases de PHP</h2>

En PHP, una función es un bloque de código reutilizable que realiza una tarea concreta.
Una clase es un modelo (plantilla) que describe objetos con propiedades y métodos, permitiendo programación orientada a objetos (POO).

---

## ➢ <u>TABLA RESUMEN RÁPIDA - FUNCIONES</u>

| Función | Descripción | Retorna | Uso Principal |
|---------|-------------|---------|---------------|
| [`is_null()`](#is_null)| Verifica si es estrictamente NULL | bool | Validación estricta de NULL |
| [`empty()`](#empty)| Verifica si está "vacío" | bool | Validar campos de formulario |
| [`isset()`](#isset) | Verifica si existe y no es NULL | bool | Comprobar $_POST, $_GET |
| [`date()`](#date) | Formatea fecha/hora | string | Mostrar fechas legibles |
| [`var_dump()`](#var_dump) | Muestra tipo y valor detallado | void | Debug y desarrollo |
| [`nl2br()`](#nl2br) | Convierte \n en `<br>` | string | Mostrar texto con saltos |
| [`htmlspecialchars()`](#htmlspecialchars) | Escapa caracteres HTML | string | Prevenir XSS |
| [`list()`](#list) | Asigna variables desde array | array | Desestructurar arrays |
| [`json_encode()`](#json_encode) | Convierte a JSON | string | APIs y AJAX |
| [`json_decode()`](#json_decode) | Convierte JSON a PHP | mixed | Leer APIs y AJAX |
| [`file_put_contents()`](#file_put_contents) | Escribe en archivo | int\|false | Guardar logs, datos |
| [`basename()`](#basename) | Extrae nombre de archivo | string | Procesar rutas |
| [`header()`](#header) | Envía cabeceras HTTP | void | Redirecciones, downloads |

---


## ➢ <u>VALIDACIÓN DE VARIABLES</u>

## `is_null()`

**Descripción:** Determina si una variable es **estrictamente NULL**. Devuelve true(o 1) solo si el valor es null y false(o nada) en caso contrario.

**Sintaxis:**
```php
is_null(mixed $var): bool
```

**Ejemplo:** 
```php
$a = 0;
echo "a is " . is_null($a) . "<br>"; <p style=" color: 'green'">// Resutado : a is 
$b = null;
echo "b is " . is_null($b) . "<br>"; // Resutado : a is 1
$c = "null";
echo "c is " . is_null($c) . "<br>"; // Resutado : a is 
$d = NULL;
echo "d is " . is_null($d) . "<br>"; // Resutado : a is 1
```

**Cuándo usar:** Cuando necesitas verificar específicamente si una variable es NULL, sin considerar otros valores "vacíos".

**Referencias:**
- https://www.php.net/manual/es/function.is-null.php
- https://www.w3schools.com/php/func_var_is_null.asp

---

## `empty()`

**Descripción:** Indica si una variable está "vacía": `"", 0, "0", null, false, [], array()`. Muy útil para formularios.

**Sintaxis:**
```php
empty(mixed $var): bool
```

**Ejemplo:**
```php
$cadena = "";
if (empty($cadena)) {
    echo "Está vacía"; //Resultado : está vacía
}
```

**Cuándo usar:** Validar campos de formulario antes de procesarlos. Es más flexible que isset().

**Referencias:**
- https://www.php.net/manual/es/function.empty.php
- https://www.w3schools.com/php/func_var_empty.asp

---

##  `isset()`

**Descripción:** Comprueba si una variable está **declarada** y es diferente de NULL. Ideal para verificar datos de formularios.
Esta función devuelve verdadero si la variable existe y no es NULL, de lo contrario devuelve falso.

**Sintaxis:**
```php
isset(mixed $var, mixed ...$vars): bool
```

**Ejemplo:**
```php
$a = 0;
// True because $a is set
if (isset($a)) {
  echo "Variable 'a' is set.<br>"; //Resultado : Variable 'a' is set.
}

$b = null;
// False because $b is NULL
if (isset($b)) {
  echo "Variable 'b' is set."; //Resultado:--
}
?>
```

**Cuándo usar:** Verificar si existen datos en $_POST, $_GET, $_SESSION antes de usarlos. Evita errores.

**Advertencia:** isset() funciona únicamente con variables. Para verificar constantes, usa `defined()`.

**Referencias:**
- https://www.w3schools.com/php/func_var_isset.asp
- https://www.php.net/manual/es/function.isset.php

---

## ➢ <u>FORMATO Y PRESENTACIÓN</u>

## `date()`

**Descripción:** Devuelve una cadena formateada según el formato indicado usando el integer timestamp (Unix timestamp) dado, o el momento actual si no se da una marca de tiempo. En otras palabras, timestamp es opcional y por defecto es el valor de time().

**Sintaxis:**
```php
date(string $format, int $timestamp = time()): string
```

**Ejemplos:**
```php
// Asumiendo: 10 de marzo de 2001, 5:16:18 pm 
date_default_timezone_set("Europe/Madrid");

echo date("F j, Y, g:i a") . "\n";                 // March 10, 2001, 5:16 pm
echo date("m.d.y") . "\n";                         // 03.10.01
echo date("j, n, Y") . "\n";                       // 10, 3, 2001
echo date("Ymd") . "\n";                           // 20010310
echo date('h-i-s, j-m-y, it is w Day') . "\n";     // 05-16-18, 10-03-01, 1631 1618 6 Satpm01
echo date('\i\t \i\s \t\h\e jS \d\a\y.') . "\n";   // it is the 10th day.
echo date("D M j G:i:s T Y") . "\n";               // Sat Mar 10 17:16:18 MST 2001
echo date('H:m:s \m \i\s\ \m\o\n\t\h') . "\n";     // 17:03:18 m is month
echo date("H:i:s") . "\n";                         // 17:16:18
echo date("Y-m-d H:i:s") . "\n";                   // 2001-03-10 17:16:18 (the MySQL DATETIME format)
```

**Cuándo usar:** Mostrar fechas de publicaciones, logs, reportes. Formato MySQL: `"Y-m-d H:i:s"`

**Referencias:**
- https://www.w3schools.com/php/func_date_date.asp
- https://www.php.net/manual/es/function.date.php

---

## `nl2br()`

**Descripción:** Inserta saltos HTML (`<br>` o `<br />`) antes de cada salto de línea (\n) en una cadena(\r\n, \n\r, \n y \r).
Más informacion sobre secuencias de escape, [aquí](https://www.php.net/manual/es/regexp.reference.escape.php)

**Sintaxis:**
```php
nl2br(string $string, bool $use_xhtml=true): string
```

**Ejemplo:**
```php
echo nl2br("Hola\nMundo");// Resultado: Hola
                            //          Mundo 
```

**Cuándo usar:** Mostrar comentarios, descripciones o texto de textarea con saltos de línea.

**Referencias:**
- https://www.w3schools.com/php/func_string_nl2br.asp
- https://www.php.net/manual/es/function.nl2br.php

---

## `htmlspecialchars()`

**Descripción:** Convierte caracteres especiales en entidades HTML.
- & (ampersand) se convierte en &amp;
- " (comillas dobles) se convierte en &quot;
- ' (comilla simple) se convierte en &#039;
- < (menor que) se convierte en &lt;
- > (mayor que) se convierte en &gt;

**Sintaxis:**
```php
htmlspecialchars(string $string): string
```

**Ejemplo:**
```php
$new = htmlspecialchars("<a href='test'>Test</a>", ENT_QUOTES);
echo $new; // Resultado: &lt;a href=&#039;test&#039;&gt;Test&lt;/a&gt;
```

**Referencias:**
- https://www.w3schools.com/php/func_string_htmlspecialchars.asp
- https://www.php.net/manual/es/function.htmlspecialchars.php

---

## ➢ <u>MANIPULACIÓN DE DATOS</u> 

## `list()`

**Descripción:** La función list() se utiliza para asignar valores a una lista de variables en una sola operación.La primera variable es obligatoria, las otras son opcionales.

**Sintaxis:**
```php
list(mixed $var1, mixed ...$vars): array
```

**Ejemplo:**
```php
$my_array = array("Dog", "Cat", "Horse");
list($a, $b, $c) = $my_array;
echo "I have several animals, a $a, a $b and a $c."; // Resultado: I have several animals, a Dog, a Cat and a Horse.
```

**Referencias:**
- https://www.php.net/manual/es/function.list.php
- https://www.w3schools.com/php/func_array_list.asp

---

## `json_encode()`

**Descripción:** Retorna la representación JSON de un valor.

**Sintaxis:**
```php
json_encode(mixed $value, int $flags = 0, int $depth = 512): string|false
```

**Ejemplo:**
```php
$age = array("Peter"=>35, "Ben"=>37, "Joe"=>43);
echo json_encode($age); // Resultado: {"Peter":35,"Ben":37,"Joe":43}
```

**Referencias:**
- https://www.w3schools.com/php/func_json_encode.asp
- https://www.php.net/manual/es/function.json-encode.php

---

## `json_decode()`

**Descripción:** Recupera una cadena codificada en JSON y la convierte en un valor de PHP.

**Sintaxis:**
```php
json_decode(
    string $json,
    ?bool $associative = null,
    int $depth = 512,
    int $flags = 0
): mixed
```

**Ejemplo:**
```php
// Como objeto
$jsonobj = '{"Peter":35,"Ben":37,"Joe":43}';
$obj = json_decode($jsonobj);
echo $obj->Peter;
echo $obj->Ben;
echo $obj->Joe; //Resultado: 353743

// Como array asociativo
$jsonobj = '{"Peter":35,"Ben":37,"Joe":43}';
var_dump(json_decode($jsonobj, true)); <p style="color='green'">//Resultado: array(3) { ["Peter"]=> int(35) ["Ben"]=> int(37) ["Joe"]=> int(43) }
```

**Referencias:**
- https://www.php.net/manual/es/function.json-decode.php
- https://www.w3schools.com/php/showphp.asp?filename=demo_json_decode3

---

## `var_dump()`

**Descripción:** Muestra información detallada de una variable: tipo, longitud y valor.

**Sintaxis:**
```php
var_dump(mixed $value, mixed ...$values): void
```

**Ejemplo:**
```php
$a = 32;
echo var_dump($a) . "<br>"; //Resultado: int(32)

$b = "Hello world!";
echo var_dump($b) . "<br>"; //Resultado: string(12) "Hello world!"

$c = 32.5;
echo var_dump($c) . "<br>"; //Resultado: float(32.5)

$d = array("red", "green", "blue");
echo var_dump($d) . "<br>"; //Resultado: array(3) { [0]=> string(3) "red" [1]=> string(5) "green" [2]=> string(4) "blue" }

$e = array(32, "Hello world!", 32.5, array("red", "green", "blue"));
echo var_dump($e) . "<br>"; //Resultado: array(4) { [0]=> int(32) [1]=> string(12) "Hello world!" [2]=> float(32.5) [3]=> array(3) { [0]=> string(3) "red" [1]=> string(5) "green" [2]=> string(4) "blue" } }

// Dump two variables
echo var_dump($a, $b) . "<br>"; //Resultado: int(32) string(12) "Hello world!"
```

**Cuándo usar:** Debug durante desarrollo. Ver estructura exacta de variables complejas.

**Referencias:**
- https://www.w3schools.com/php/func_var_var_dump.asp
- https://www.php.net/manual/es/function.var-dump.php

---

## ➢ <u>ARCHIVOS Y SISTEMA</u>

## `file_put_contents()`

**Descripción:** Escribe contenido en un archivo. Crea el archivo si no existe, o lo sobrescribe por defecto.
Esta función sigue estas reglas al acceder a un archivo:
 - Si se ha configurado FILE_USE_INCLUDE_PATH, compruebe la ruta de inclusión para encontrar una copia del nombre de archivo.
 - Crea el archivo si no existe.
 - Abre el archivo
 - Bloquea el archivo si LOCK_EX está activado.
 - Si FILE_APPEND está definido, se desplaza al final del archivo. De lo contrario, se borra el contenido del archivo.
 - Escribe los datos en el archivo
 - Cierra el archivo y libera cualquier bloqueo.
  
Utilizar FILE_APPEND para evitar eliminar el contenido existente del archivo.

**Sintaxis:**
```php
file_put_contents(
    string $filename,
    mixed $data,
    int $flags = 0,
    ?resource $context = null
): int|false
```

**Ejemplo:**
```php
// Sobrescribir archivo
file_put_contents("log.txt", "Nuevo contenido\n");

// Añadir al final (append)
file_put_contents("log.txt", "Acceso realizado\n", FILE_APPEND);
```

**Importante:** Verifica permisos de escritura. Retorna `false` si falla.

**Referencias:**
- https://www.php.net/manual/es/function.file-put-contents.php
- https://www.w3schools.com/php/func_filesystem_file_put_contents.asp

---

## `basename()`

**Descripción:** Devuelve el nombre del componente final de una ruta.
**Nota:**
basename() actúa de manera ingenua y no tiene conocimiento del sistema de archivos subyacente o de los componentes de una ruta tales como "..".

**Sintaxis:**
```php
basename(string $path, string $suffix = ""): string
```

**Ejemplo:**
```php
echo basename("/var/www/html/index.php");     // index.php
echo basename("C:\\Windows\\System32\\cmd.exe"); // cmd.exe

// También elimina extensión si se especifica
echo basename("/var/www/html/index.php", ".php"); // index
```

**Cuándo usar:** Procesar rutas de archivos subidos, mostrar nombres sin ruta completa.

**Referencias:**
- https://www.php.net/manual/es/function.basename.php
- https://www.w3schools.com/php/func_filesystem_basename.asp

---

## ➢ <u>HTTP Y CABECERAS</u>

## `header()`

**Descripción:** Envía cabeceras HTTP al navegador. 
header() permite especificar el encabezado HTTP string al enviar los ficheros HTML. Consúltese » HTTP/1.1 Specification para obtener más información sobre los encabezados HTTP.

Nunca se olvide que header() debe ser llamada antes de que se envíe cualquier contenido, ya sea por líneas HTML habituales en el fichero, o por salidas PHP. Un error muy común es leer un fichero con include o require, y dejar espacios o líneas vacías, que producirán una salida antes de que la función header() sea llamada. El mismo problema existe con los ficheros PHP/HTML estándar.

**Sintaxis:**
```php
header(string $header, bool $replace = true, int $response_code = 0): void
```

**Ejemplos:**
```php
//Esta cabecera pide al navegador que muestre una ventana de usuario y contraseña.
//“Basic” indica que es autenticación HTTP Basic.
// Realm="Contenido restringido" es el texto que aparece en el cuadro de login del navegador.
header('WWW-Authenticate: Basic Realm="Contenido restringido"');
//Esto envía al navegador el código de estado 401, que significa: “No autorizado – debes identificarte”.
header('HTTP/1.0 401 Unauthorized');
```

**Error común:** Si ya se envió contenido (HTML, espacios), dará error "Headers already sent".(Puede darse este error en PLESK)

**Referencias:**
- https://www.php.net/manual/es/function.header.php
- https://www.w3schools.com/php/func_network_header.asp

---
