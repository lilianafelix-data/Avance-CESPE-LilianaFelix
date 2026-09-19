
# Avance del módulo CESPE (bitácora de semana y media)

## Estudio realizado
- Revisé la página oficial de CESPE para entender cómo aparecen las noticias y avisos.  
- Analicé qué librerías serían necesarias para el web scraping (requests, BeautifulSoup, json).  
- Consulté documentación y artículos sobre scraping, como el blog de HubSpot por mencionar uno de los que lei para adentrarme un poco mas en el tema de web scraping.  
- Identifiqué que CESPE no siempre incluye el año en las fechas, por lo que se requiere usar la fecha de referencia (`retrieved_at`).  

## Trabajo colaborativo
- Me puse de acuerdo con los demás extractores para definir la estructura del JSON de salida.  
- Revisamos con el equipo de Request cómo les proporcionaríamos los URLs y cómo ellos nos devolverían los textos limpios.  
- Discutimos que cada página es diferente: algunas usan RSS para obtener URLs, otras no; algunas tienen hasta 20 noticias, otras solo 4.  
- Acordamos un formato común de salida para que todos los módulos trabajen de manera uniforme.

## Pruebas de código
Probé funciones para:
- Detectar días de la semana y números asociados.  
- Extraer fechas con y sin año.  
- Identificar colonias y vías (avenidas, calles, bulevares).  
- Extraer enlaces de la página de CESPE y filtrarlos por palabras clave como “aviso”, “corte” o “suspensión”.

  ## Errores que me salieron
- Al principio los URLs no se guardaban en el JSON que creé. Después descubrí que era porque no estaba filtrando bien los enlaces.  
- Lo resolví agregando condiciones en el código con palabras clave como “suspensión”**, “corte”, **“aviso”, que son las que normalmente aparecen en los títulos de los avisos.  
- También tuve un SyntaxError por un paréntesis que no cerré.  
- Algunos enlaces estaban vacíos o repetidos, así que tuve que filtrarlos mejor.  
- Problemas al normalizar fechas sin año, que resolví usando la fecha de referencia (`retrieved_at`).

Ejemplo simplificado de prueba para la extracción de las url de la pagina:

```python
from bs4 import BeautifulSoup
import requests

url = "https://www.cespe.gob.mx/public/Noticias?page=1"
html = requests.get(url).text
soup = BeautifulSoup(html, "html.parser")

links = [a["href"] for a in soup.find_all("a", href=True)]
print(links[:5])  # muestra los primeros 5 enlaces





