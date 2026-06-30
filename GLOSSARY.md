# Guía de traducción ES — glosario y convenciones

Leé esto antes de traducir cualquier nota. Esta guía hereda el registro y la mayoría de la terminología de la del [atlas I](https://github.com/ldamoredev/lowlevel-notes/blob/main/GLOSSARY.md) — no la duplica, solo agrega los términos nuevos que introduce este atlas (sistemas de red, bases de datos, parsing). Si un término ya está resuelto en la guía del atlas I, usá esa misma resolución acá.

## Arquitectura de la traducción (igual que el atlas I)

Mismo mecanismo de overlay: un archivo ES vive en la misma ruta relativa bajo `content/es/`. Si falta, `build.py` muestra la fuente EN con un banner de "traducción pendiente" — nunca una página rota. Workflow:

1. Listá las notas EN sin overlay ES.
2. Creá el archivo ES correspondiente con la misma ruta relativa.
3. `python3 build.py` y verificá `(unresolved links: 0)`.

## Registro

Igual que el atlas I: español rioplatense, voseo (`Usá`, `Pensá`, `Tené en cuenta` — nunca tú/usted), densidad técnica equivalente al original, código/identificadores/flags siempre en inglés y en monospace.

## Terminología nueva (EN → ES) — específica de este atlas

| EN | ES (preferido) | Nota |
|---|---|---|
| build queue | cola de build | en vez de "ruta de aprendizaje" del atlas I |
| spine project | proyecto vertebrador | mismo término que el atlas I |
| warm-up build | proyecto de calentamiento | — |
| event loop | event loop | dejar en inglés, término establecido |
| keep-alive | keep-alive | dejar en inglés |
| thread pool | thread pool | dejar en inglés |
| lock-free | lock-free | dejar en inglés |
| false sharing | false sharing | dejar en inglés |
| write-ahead log (WAL) | write-ahead log (WAL) | dejar en inglés, glosar la sigla la primera vez |
| crash recovery | crash recovery | dejar en inglés |
| durability | durabilidad | traducir |
| B-Tree / B+Tree | B-Tree / B+Tree | dejar en inglés, es nombre propio de estructura |
| copy-on-write | copy-on-write | dejar en inglés |
| query planner/executor | planner/executor | dejar en inglés |
| backtracking | backtracking | dejar en inglés |
| state machine | máquina de estados | traducir |
| content-addressed storage | almacenamiento direccionado por contenido | traducir |
| commit graph | grafo de commits | traducir parcialmente, "commit" queda |
| load testing | benchmarking bajo carga / load testing | cualquiera de los dos, según contexto |
| job control | manejo de jobs | traducir parcialmente |
| foreground/background | foreground/background | dejar en inglés (jerga de shell establecida) |

## Reglas finas (igual que el atlas I)

- Primera mención bilingüe: glosá el término en inglés entre paréntesis la primera vez que aparece en una nota si no es de uso 100% establecido.
- Nunca traduzcas el *target* de un wikilink, solo el *label*: `[[lowlevel-ii/mini-git/index|Mini Git]]` se traduce como `[[lowlevel-ii/mini-git/index|Mini Git]]`, no se toca la ruta.
- Espejá la cantidad y el orden de encabezados `##` del original — el TOC y los anchors dependen de eso.
- Las citas en `## Sources` quedan en su idioma original, no se traducen.
