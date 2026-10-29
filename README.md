# Contenido clínico de ConsultaMed

La app combina su **contenido integrado** (medicamentos, guías y CIE-10) con **paquetes de contenido** en JSON. Un paquete puede agregar, reemplazar o retirar medicamentos y guías, y agregar códigos CIE-10, sin tener que recompilar la app.

## Cómo se actualiza

1. Publica esta carpeta en un repositorio (por ejemplo, GitHub).
2. En la app: **Perfil → Contenido clínico y actualizaciones**, pega la dirección *raw* del `manifest.json`, por ejemplo:
   `https://raw.githubusercontent.com/<usuario>/<repositorio>/main/Contenido/manifest.json`
3. La app busca actualizaciones una vez por semana (o con el botón **Buscar**). Muestra las versiones nuevas y **solo las instala si tú lo confirmas**.
4. Para publicar una actualización: edita o crea el paquete, sube su `version` y actualiza la entrada en `manifest.json`.

Las rutas `url` del manifiesto pueden ser relativas al propio manifiesto.

## Formato del paquete (`formatVersion` 1)

```json
{
  "format": "consultamed-content",
  "formatVersion": 1,
  "id": "actualizacion-2027-01",
  "version": "2027.01",
  "title": "Actualización de enero de 2027",
  "published": "2027-01-15",
  "notes": "Qué cambió y por qué.",
  "drugs": [ { "id": "paracetamol", "name": "Paracetamol", "group": "analgesicos", "adult": "…", "references": [ { "title": "…", "url": "https://…", "year": "2027" } ] } ],
  "guides": [ { "id": "hta", "title": "Hipertensión arterial sistémica", "area": "cardiologia", "source": "…", "icd10": ["I10"], "sections": [ { "title": "…", "points": ["…"] } ], "regimens": [ … ], "references": [ … ], "reviewed": "enero de 2027" } ],
  "icd10": [ { "code": "U07.1", "description": "COVID-19, virus identificado" } ],
  "removedDrugIDs": [],
  "removedGuideIDs": []
}
```

- Un medicamento o guía con el mismo `id` que uno integrado **lo reemplaza**; con un `id` nuevo, **se agrega**.
- `removedDrugIDs` y `removedGuideIDs` retiran contenido (por ejemplo, un fármaco que salió del mercado).
- Los campos no obligatorios pueden omitirse. `paquetes/consultamed-base.json` es un ejemplo completo con todo el contenido integrado: sirve como plantilla.
- Valores de `group`: analgesicos, antibioticos, antivirales, antiparasitarios, gastro, cardiovascular, metabolico, respiratorio, alergia, neuro, obstetricia, dermatologia, urgencias, otros.
- Valores de `area`: general, medicinaInterna, urgencias, cardiologia, neumologia, nefrologia, gastroenterologia, infectologia, endocrinologia, pediatria, ginecoObstetricia, neurologia, psiquiatria, dermatologia.

## Catálogo CIE-10 completo

La app trae ~360 códigos frecuentes. Para el catálogo completo, importa un CSV con columnas de código y descripción (**Contenido clínico → Importar paquete o CIE-10**). Fuente recomendada: el catálogo oficial de la DGIS / CEMECE de la Secretaría de Salud.

## Calculadoras

Las fórmulas de las calculadoras están en el código (`Models/Clinical/CalculatorCatalog.swift`) porque requieren lógica; sus referencias se muestran en cada calculadora.

## Advertencia

Este contenido es de apoyo y no sustituye el juicio clínico. Cada actualización debe revisarse contra la fuente original antes de publicarse.
