# 📦 Módulos y Paquetes

  

## 🧠 Módulos

- Cualquier archivo `.py` puede ser importado

- `import`, `from x import y`, `as`

  

## 🧠 Paquetes

- Carpetas con `__init__.py`

- Organización de código en proyectos grandes

  

## 🧪 Ejemplo

```python

# archivo: utilidades.py

def saludar(): print("Hola")

  

# otro archivo

from utilidades import saludar

saludar()

```

  

## ✅ Mini desafíos

1. Crear un módulo con funciones matemáticas.

2. Usar un paquete estándar (ej. `math`, `random`).

3. Importar con alias (`import math as m`).

  

## 📌 Tips

- Usa `if __name__ == "__main__"` para scripts ejecutables

- Los módulos ayudan a reutilizar código