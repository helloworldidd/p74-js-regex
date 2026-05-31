# Guía de **expresiones regulares**

**Indice**
```
1. Qué son
1.1 Definición
1.2 Sintaxis base
1.3 Símbolos más usados
1.4 Modificadores

2. Metodos mas usados
2.1 Métodos
2.1 replace()
2.2 `replace()`
2.3 `test()`
2.4 `match()`
2.5 `search()`
2.6 `split()`

3. Ejemplos
```

---

## 1. Qué son

### 1.1 Definición

**RegEx**: patrones para buscar, validar o limpiar texto.



### 1.2 Sintaxis base

`/patron/modificador`

Ejemplo:
`/\D/g` Significa: buscar todo lo que **no sea número**, en todo el texto.

### 1.3 Símbolos más usados

```js
\d    número del 0 al 9
\D    todo lo que NO sea número

\w    letras, números y _
\W    todo lo que NO sea letra, número o _

\s    espacios
\S    todo lo que NO sea espacio

.     cualquier carácter

^     inicio del texto
$     final del texto

+     una o más veces
*     cero o más veces
?     opcional

{3}   exactamente 3 veces
{3,}  mínimo 3 veces
{3,8} entre 3 y 8 veces

[abc]     permite a, b o c
[a-z]     letras de la a a la z
[0-9]     números del 0 al 9
[^abc]    todo excepto a, b o c
```

### 1.4 Modificadores

```txt
g   global, busca todos
i   ignora mayúsculas/minúsculas
m   múltiples líneas
```





---

## 2. Metodos mas usados




### 2.1 Métodos

``` js
replace() // limpiar
test()    // validar
match()   // encontrar
search()  // buscar posición
split()   // dividir
```





### 2.1 replace()

- `texto.replace(regex, "")`
- **reemplazar texto usando regex**
- _Limpiar texto, Eliminar caracteres, Formatear datos_

```js

"abc12**3".replace(/\D/g, "")

// resultado

"123"
```


### 2.2 `replace()`

- `regex.test(texto)`
- **reemplazar texto usando regex**
-__Limpiar texto, Eliminar caracteres, Formatear datos__


### 2.3 `test()`
- **validar si un texto cumple un patrón**
- __Validar email, teléfono, URL,  RUT__
```js
/^\d+$/.test("123")

// resultado: true


/^\d+$/.test("123abc")
// resultado: false
```


### 2.4 `match()`
- **encontrar coincidencias en texto**
- __Buscar palabras, Extraer números, fechas, correos__
`texto.match(regex)`

```js
"abc123xyz".match(/\d/g)
// resultado   ["1", "2", "3"]


"Vue y React".match(/Vue/g)

// resultado  ["Vue"]
```

### 2.5 `search()`
- **posición de la primera coincidencia**
- __Saber si existe una palabra, Ubicar una coincidencia__


`texto.search(regex)`

```js
"Hola Vue".search(/Vue/)

// resultado  5

"Hola Vue".search(/React/)

// resultado   -1
```











### 2.6 `split()`
- **dividir un texto usando regex**
- __Separar CSV, Separar fechas, Separar etiquetas__




`texto.split(regex)`

```js
"Juan,Pedro,María".split(/,/)

//resultado ["Juan", "Pedro", "María"]

"2026-05-31".split(/-/)
// resultado ["2026", "05", "31"]
```









---

## 3. Ejemplos



```js
// Solo números
texto.replace(/\D/g, "")

//    \D = cualquier carácter que NO sea número
//    g  = buscar todos

// resultado
"abc123" → "123"
"$1.500" → "1500"
```


```js
// Solo letras y espacios
texto.replace(/[^a-zA-ZáéíóúÁÉÍÓÚñÑ\s]/g, "")

//    [^ ] = todo excepto
//    a-z  = letras minúsculas
//    A-Z  = letras mayúsculas
//    \s   = espacios

// resultado
"Juan123 Pérez!!" → "Juan Pérez"
"Patricio_2026" → "Patricio"
```


```js
// Validar email simple
/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)

//     ^      = inicio
//     [^\s@] = cualquier cosa excepto espacio o @
//     +      = uno o más
//     @      = arroba obligatoria
//     \.     = punto obligatorio
//     $      = fin


//  válidos:
//  patricio@gmail.com
//  hola@empresa.cl

//  inválidos:
//  patricio
//  @gmail.com
//  hola@
```



```js
// Validar URL simple
/^(https?:\/\/)?([\w-]+\.)+[\w-]{2,}(\/.*)?$/i.test(url)

//    https? = http o https
//    ?      = opcional
//    \w     = letras o números
//    {2,}   = mínimo 2 caracteres
//    i      = ignora mayúsculas/minúsculas

// válidas:
// https://google.com
// http://github.com

// inválidas:
// google
// https://
// hola mundo
```



```js
// Validar solo números
/^\d+$/.test(valor)

//    ^   = inicio
//    \d  = número
//    +   = uno o más
//    $   = fin

// válidos:
// 123
// 456789

// inválidos:
// 123a
// 12-34
// abc
```

```js
// Validar mínimo 3 letras
/^[a-zA-ZáéíóúÁÉÍÓÚñÑ\s]{3,}$/.test(nombre)

// {3,} = mínimo 3 caracteres

// válidos:
// Juan
// María
// Pedro

// inválidos:
// A
// Jo
// 12
```

```js
// Validar teléfono chileno (9 dígitos)
/^\d{9}$/.test(telefono)

// {9} = exactamente 9 caracteres


// válidos:
// 912345678
// 987654321

// inválidos:
// 123
// 91234567890
// abc123456
```

```js
// Validar RUT (formato básico)
/^[0-9kK.-]+$/.test(rut)

//    0-9 = números
//    kK  = permite k o K
//    .   = punto
//    -   = guión
//    +   = uno o más

// válidos:
// 12345678-9
// 12.345.678-5
// 9876543-K

// inválidos:
// abc
// 12@34
```


```js
// Buscar palabra Vue dentro de un texto
/.*vue.*/i.test(texto)

//    // .* = cualquier cosa
// vue = palabra buscada
// i = ignora mayúsculas/minúsculas

// coincide:
// Vue
// vue.js
// Aprendiendo Vue
// VUE
```




```js
// Extraer todos los números
texto.match(/\d/g)

//    \d = número
//    g  = buscar todos
//    */

// "abc123xyz456"
// resultado
// ["1","2","3","4","5","6"]
```








