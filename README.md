# Avisos de Dársena

La app lee `notices.json` de la rama `main` al abrirse y al volver a primer plano.

https://raw.githubusercontent.com/ferrosaco/darsena-avisos/main/notices.json

GitHub puede tardar un par de minutos en servir el archivo nuevo.

## Actualización

Hay dos umbrales, los dos opcionales:

- `minimumVersion`: si la app instalada es más antigua, sale un aviso que se puede cerrar.
- `requiredVersion`: si la app instalada es más antigua, la app se bloquea hasta actualizar.
- `required: true` es el modo antiguo: trata `minimumVersion` como bloqueo. Las builds nuevas miran primero `requiredVersion`.
- La compilación 62 necesita que `required` esté presente. Si falta, ignora el archivo entero. Con `required: false` el aviso de `minimumVersion` se puede cerrar.

`messages` y `requiredMessages` llevan el texto en `es`, `gl` y `en`. Si falta el idioma, se usa el español.
`message` en un solo idioma sigue valiendo: las builds anteriores solo leen ese campo.

## Afectaciones

El aviso se muestra al abrir una parada o una línea que coincida. Una línea afecta también a las paradas por las que pasa.
El texto va en `messages` (`es`, `gl`, `en`). `message` es el respaldo de una sola frase.
`from` y `until` son fechas ISO 8601 con zona horaria. El aviso solo se muestra entre esas dos horas. Si falta `from`, se muestra desde que se publica. Pasada `until`, desaparece.
La compilación 63 y las anteriores ignoran `from` y mostrarían el aviso en cuanto esté en el archivo. Un aviso programado solo debe publicarse cuando la app instalada sea la 64 o posterior.
`url` es el botón «Saber más».
La aspa lo oculta solo en esa ficha. Al volver a abrir una parada o línea afectada, vuelve a salir.

```json
{
  "id": "linea-4",
  "messages": {
    "es": "La línea 4 no para en Puerta Real hasta el viernes.",
    "gl": "A liña 4 non para na Porta Real ata o venres.",
    "en": "Line 4 does not stop at Puerta Real until Friday."
  },
  "url": "https://ejemplo.com/aviso",
  "from": "2026-10-10T00:00:00+02:00",
  "until": "2026-10-11T00:00:00+02:00",
  "lineIds": [4],
  "stopIds": [1204]
}
```

`lineIds` y `stopIds` son los identificadores internos. La 3 es `300` y la 5 es `500`. Esos dos campos siguen avisando solo en la ficha de una parada o una línea del bus urbano.

## Pestañas

`modes` dice en qué pestañas sale el aviso: `bus`, `bike`, `taxi`, `train` o `tmg`. Se muestra arriba de esa pestaña. En bici, tren y TMG también sale al abrir una ficha. Un aviso de bus urbano que solo lleva `lineIds` o `stopIds` no aparece en las demás pestañas.
La compilación 64 y las anteriores ignoran `modes`. Un aviso dirigido a otra pestaña solo lo ve la 65 o una posterior.

```json
{
  "id": "renfe-carretera",
  "messages": {
    "es": "Entre el 5 y el 12 de noviembre el servicio de Renfe se prestará por carretera.",
    "gl": "Entre o 5 e o 12 de novembro o servizo de Renfe prestarase por estrada.",
    "en": "Between 5 and 12 November the Renfe service will be provided by road."
  },
  "url": "https://grupo.renfe.com/es/es/sala-de-prensa/noticias/2026/10/renfe-modifica-temporalmente-servicio-a-coruna",
  "from": "2026-10-08T00:00:00+02:00",
  "until": "2026-11-13T00:00:00+01:00",
  "modes": ["train"]
}
```
