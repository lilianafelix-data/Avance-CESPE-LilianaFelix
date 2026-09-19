# Avance-CESPE-LilianaFelix

# Módulo Extractor CESPE

## Objetivo
Este módulo se encarga de trabajar con los avisos publicados en la página oficial de CESPE.  
Mi responsabilidad es extraer los enlaces (URLs) de las noticias y pasárselos al módulo Request, para que ellos limpien el HTML y me devuelvan el texto plano.  
Con ese texto limpio, yo aplico las funciones necesarias para detectar fechas y ubicaciones (colonias, calles, avenidas) que aparecen en los avisos.

## Flujo de trabajo
1. El módulo CESPE obtiene los URLs de la página oficial.  
2. Los URLs se entregan al módulo Request.  
3. Request devuelve el texto limpio de cada aviso.  
4. Con funciones propias (`procesar_y_evaluar_dias`, `extraer_fecha`, `extraer_via`, `extraer_colonias`) se identifican los datos clave.  
5. Se arma un JSON de salida con la información encontrada.

## Librerías utilizadas
- `BeautifulSoup` → para analizar el HTML y extraer los enlaces.  
- `json` → para guardar los resultados en un formato ordenado.  

## Funciones principales
- **procesar_y_evaluar_dias** → detecta días de la semana y números asociados.  
- **extraer_fecha** → busca fechas completas o parciales y usa el año de referencia si no aparece.  
- **extraer_via** → identifica avenidas, calles o bulevares.  
- **extraer_colonias** → detecta colonias mencionadas en el aviso.  
- **extract_fields** → combina los datos encontrados y arma el JSON final.  
- **extractor_links** → obtiene los enlaces de la página y guarda los que son avisos relevantes.

## Ejemplo de salida JSON
```json
{
  "source": "CESPE",
  "url": "https://www.cespe.gob.mx/public/Noticias/",
  "data": {
    "fecha": "2026-09-09",
    "dia": "miércoles",
    "colonia": "Centro",
    "avenida": "Reforma"
  },
  "confidence": 0.85
}

