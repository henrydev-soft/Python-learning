# 🛑 Manejo de Errores y Excepciones

  

## 🧠 Bloque try-except

```python

try:

    x = int(input("Ingresa un número: "))

except ValueError:

    print("Eso no es un número.")

```

  

## 🧠 Opciones adicionales

- `else`: si no hubo excepción

- `finally`: siempre se ejecuta

- Capturar múltiples errores: `except (TypeError, ZeroDivisionError)`

  

## ✅ Mini desafíos

1. Script que maneje división por cero.

2. Validación de input numérico usando try-except.

3. Crea tu propia excepción con `raise`.

  

## 📌 Tips

- Maneja solo lo necesario, no uses `except:` sin tipo

- Siempre muestra mensajes claros al usuario