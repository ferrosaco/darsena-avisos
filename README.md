# Avisos de Dársena

La app lee `notices.json` de la rama `main` al abrirse y al volver a primer plano.
La URL es:

https://raw.githubusercontent.com/ferrosaco/darsena-avisos/main/notices.json

GitHub puede tardar un par de minutos en servir el archivo nuevo.

## Actualización

Sube `minimumVersion` por encima de la versión publicada para que salga el popup.
`required: true` no se puede cerrar: solo lleva a la tienda.
`required: false` se puede posponer hasta la próxima vez que se abra la app.
`message` es opcional. Si lo omites, la app pone un texto por defecto.

## Afectaciones

Cada aviso sale en rojo al abrir una parada o una línea que coincida.
Una línea afecta también a las paradas por las que pasa.
`until` es una fecha ISO 8601 con zona horaria. Pasada esa hora, el aviso desaparece aunque siga en el archivo.
`url` es el botón «Saber más». Si no hay URL, solo se muestra el texto.

```json
{
  "id": "linea-4",
  "message": "La línea 4 no para en Puerta Real hasta el viernes.",
  "url": "https://ejemplo.com/aviso",
  "until": "2026-10-10T22:00:00+02:00",
  "lineIds": [4],
  "stopIds": [1204]
}
```

`lineIds` y `stopIds` son los identificadores que ya usa la app. Puedes dejar uno de los dos vacío.
