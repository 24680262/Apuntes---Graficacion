# Representación y trazo le líneas y poligonos

Algoritmos de Trazo de Líneas
Algoritmo DDA (Digital Differential Analyzer) Calcula puntos intermedios de una línea usando incrementos decimales. Simple pero con errores de redondeo acumulados.

Algoritmo de Bresenham Más eficiente que DDA. Usa solo aritmética entera para determinar el píxel más cercano a la línea real. Es el estándar en gráficos rasterizados.

Polígonos
Un polígono regular de n lados tiene todos sus vértices equidistantes del centro. Se calcula con trigonometría como se mostró en la sección 1.3.

Práctica: Dibujo de un Polígono en Blender
```python
import bpy
import math

def crear_poligono_2d(nombre, lados, radio):
    # Crear una nueva malla y un nuevo objeto
    malla = bpy.data.meshes.new(nombre)
    objeto = bpy.data.objects.new(nombre, malla)
    
    # Vincular el objeto a la escena actual
    bpy.context.collection.objects.link(objeto)
    
    vertices = []
    aristas = []
    
    # Cálculo de vertices usando coordenadas polares a cartesianas
    for i in range (lados):
        angulo = 2 * math.pi * i / lados
        x = radio * math.cos(angulo)
        y = radio * math.sin(angulo)
        vertices.append((x, y, 0)) # Z = 0 para mantenerlo en 2D
    
    #Definir las conexiones (aristas) entre los vertices
    for i in range (lados):
        aristas.append((i, (i + 1) % lados))
        
    # Cargar los datos en la malla
    malla.from_pydata(vertices,aristas, [])
    malla.update()

# Limpiar la escena antes de empezar
bpy.ops.object.select_all(action="SELECT")
bpy.ops.object.delete()

# Llamada a la funcion: Un hexagono de radio 5
crear_poligono_2d("Poligono2D", lados=6, radio=3)
```python
