# 🔢 Tipos de Datos en Python

## 🧠 Conceptos clave

- Python tiene tipado dinámico (no declaras el tipo, el intérprete lo infiere).
- Tipos primitivos más usados:
  - `int`: enteros
  - `float`: decimales
  - `str`: texto
  - `bool`: verdadero/falso
  
- Tipos derivados útiles:
  - `list`, `tuple`, `set`, `dict` (se profundiza en otra nota)


## 🔍 Ejemplos básicos
```python
# Números
edad = 30         # int
altura = 1.75     # float

# Cadenas
nombre = "Henry"
# f-string (formatted string literals)
saludo = f"Hola, {nombre}"

# Booleanos
activo = True
es_mayor = edad >= 18
```


## 🔁 Conversión entre tipos

```python
# De string a número
numero = int("123")
decimal = float("3.14")

# De número a string
texto = str(42)

# Booleanos
bool(0)     # False
bool(3.14)  # True
bool("")    # False
```

  
### 📌En Python los String son Inmutables

Significa que **una vez creado, un string no puede cambiar su contenido**.  No puedes modificar una letra o parte del string directamente.

#### 🧪 Ejemplo claro:


```python
texto = "Hola"
texto[0] = "M"    # ❌ Esto lanza un error

#TypeError: 'str' object does not support item assignment
```

#### 🧠 ¿Entonces cómo se modifican los strings? 
**No se modifican.** Lo que haces es **crear un nuevo string**.


```python
texto = "Hola"
nuevo = "M" + texto[1:]
print(nuevo)  # "Mola"
```

#### 📦 ¿Por qué son inmutables?

- ✅ Son **seguros**: puedes usarlos como claves en diccionarios o en sets.

- 🧠 Mejoran el rendimiento: al no cambiar, Python puede **reutilizarlos internamente**.

- 🛡️ Evitan efectos secundarios raros al pasarlos entre funciones.

#### 🧠 Los String pueden tener múltiples Líneas
Las cadenas de string se pueden declarar con múltiples líneas usando `"""`

```python
# Multilínea
s2 = """Esto
es
multilínea"""
```

### 📌En Python los String se pueden indexar

Esto quiere decir que podemos acceder a los caracteres de un string con índices a manera de lista. 

```python
# acceder a caracteres
texto = "Hola Mundo"

  
print(texto[0]) #H
print(texto[1]) #o
print(texto[-0]) #H
print(texto[-2]) #d 
print(texto[0:3]) #Hol
print(texto[:4]) #Hola
print(texto[4:]) # Mundo
```

### 🎯 f-string

- Código cómo `f"Hola, {nombre}` es una forma moderna y muy legible de interpolar variables dentro de una cadena. 
- Esa `f` antes de las comillas le dice a Python: “Ey, lo que venga entre llaves `{}` dentro de esta cadena, **evalúalo como código** y reemplázalo por su valor.”
- Puedes meter **expresiones completas**, no solo variables:

```python
# Es posible meter expresiones completas, no solo variables
edad = 30
print(f"El doble de tu edad es {edad * 2}")

# Puedes aplicar formato directo:
pi = 3.141592
print(f"Pi redondeado: {pi:.2f}")  # -> Pi redondeado: 3.14
```

| Expresión f-string    | Resultado                |
| --------------------- | ------------------------ |
| `f"{2 + 3}"`          | `'5'`                    |
| `f"{nombre.upper()}"` | `'HENRY'`                |
| `f"{100/3:.2f}"`      | `'33.33'`                |
| `f"{'⚡' * 3}"`        | `'⚡⚡⚡'`                  |
| `f"{variable!r}"`     | Llama a `repr(variable)` |

- ¿Qué es `repr()`?: `repr()` es una **función incorporada de Python** que devuelve una **representación textual exacta y sin ambigüedades** de un objeto, lo más parecida posible a cómo se escribiría en código.

### Diferencia entre `str()` y `repr()`

|Función|Uso común|Resultado|
|---|---|---|
|`str()`|Representación amigable para humanos|`"Hola"`|
|`repr()`|Representación precisa para debugging|`"'Hola'"`|

```python
nombre = "Henry"
print(f"Nombre: {nombre}")      # Nombre: Henry
print(f"Nombre: {nombre!r}")    # Nombre: 'Henry'
```

Nota cómo `repr()` **incluye las comillas**, porque eso es lo que Python usaría si imprimiera ese valor en el intérprete.
  
## ⚙️ ¿Cuándo usar `repr()`?

- Cuando estás depurando y quieres ver si hay espacios, caracteres raros, comillas, etc.
- Para imprimir objetos que has definido tú y tienen un `__repr__()` útil.
- Para logs o salidas internas que no son para el usuario final.

### 🤯 Extra nerd (opcional)

Cuando creas tus propias clases, puedes definir `__str__()` y `__repr__()` para controlar qué se imprime:

```python
class Usuario:
    def __init__(self, nombre):
        self.nombre = nombre

    def __str__(self):
        return f"Usuario: {self.nombre}"

    def __repr__(self):
        return f"Usuario('{self.nombre}')"

u = Usuario("Henry")
print(str(u))   # Usuario: Henry
print(repr(u))  # Usuario('Henry')
```


## 🥊 `==` vs `is` en Python

| Comparador | ¿Qué compara?                                          | Resultado                    |
| ---------- | ------------------------------------------------------ | ---------------------------- |
| `==`       | **Valor** del objeto                                   | ¿Son iguales?                |
| `is`       | **Identidad** del objeto (misma referencia en memoria) | ¿Son el mismo objeto exacto? |
### 🧪 Ejemplo 1: Comparando valores

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b)  # True (el contenido es igual)
print(a is b)  # False (no son el mismo objeto)
```
### 🧪 Ejemplo 2:  Reutilización de objetos pequeños

```python
x = 1000
y = 1000
print(x == y)  # True
print(x is y)  # False (probablemente)

x = 5
y = 5
print(x is y)  # True (caché de enteros pequeños)
```
Python **recicla** algunos objetos inmutables pequeños (como `int` de -5 a 256 o strings cortos). Por eso, a veces `is` parece funcionar… y eso confunde más.

### 🎯 ¿Por qué se confunden?

- Porque para valores simples (`int`, `str` pequeños), `==` y `is` **pueden parecer lo mismo**, pero no lo son.

- Porque otros lenguajes como JavaScript usan `==` y `===`, lo que complica el cambio de chip.

- Porque `is` suena como “es igual”, pero significa “es el _mismo objeto_”.

#### Mal uso típico

```python
x = "hola"
if x is "hola":   # ¡NO! Comparar con `is` para strings es arriesgado
   print("Saludo detectado")
```

####  Mejor:

```python
if x == "hola":
   print("Saludo detectado")
```

#### ¿Cuándo usar `is` entonces?

Solo en casos de comprobar si dos variables apuntan exactamente al mismo objeto en memoria, por ejemplo para comparar con `None`. 

```python
if variable is None:
    ...
```

## 🧠 Regla de oro para que nunca te confundas:

> 👉 **Usa `==` para comparar valores. Usa `is` solo cuando quieres saber si son el mismo objeto exacto.**


## ✅ Mini desafíos

1. Programa que pida tu edad y diga si puedes votar.

2. Conversión de temperatura y clasificación de clima.

3. ¿Qué retorna `bool("False")` y `bool([])`?

## ⚠️ Errores comunes

- Confundir `==` con `is`, El primero compara valor del objeto y el segundo compara identidad *referencia en memoria*.
- `input()` siempre retorna string, esta es una función integrada que permite a los programas recibir datos ingresados por el usuario a través del teclado. 

## 📌 Tips para recordar

- `type(x)` para saber el tipo.

- Strings son inmutables.

- `isinstance(x, tipo)` para verificar tipos.

  

## 📚 Recursos

- [https://docs.python.org/3/library/stdtypes.html](https://docs.python.org/3/library/stdtypes.html)

- [https://gto76.github.io/python-cheatsheet/](https://gto76.github.io/python-cheatsheet/)