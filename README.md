# AI-ku_Knowledge

Dataset de conocimiento en formato **JSONL** (fine-tuning tipo SFT) en **español**, construido para el asistente **AI-ku**. Corte de conocimiento: **2026-10-04**. Compilado y verificado el 2026-10-05 con investigación web en vivo de todos los dominios.

## Dominios y prioridad

| Dominio | Filas | % filas | % esfuerzo declarado | Notas |
|---|---|---|---|---|
| `hatsune_miku` (ecosistema Vocaloid) | 124 | 51.0% | **40% — PRIORIDAD ABSOLUTA** | Historia, software/voicebanks, Crypton/Piapro/KARENT, conciertos, juegos, productores, canciones, memes, licencias, canon vs fanon, ecosistema (Rin/Len, Luka, MEIKO, KAITO, Teto, motores), tecnología |
| `ia_2024_2026` | 61 | 25.1% | 30% | Cronología verificada en vivo: OpenAI, Anthropic, Google/DeepMind, DeepSeek, Kimi/Moonshot, Qwen/Alibaba, GLM/Zhipu, Meta, NVIDIA, Mistral, xAI, otros; agentes, coding, reasoning, multimodal |
| `uma_musume` | 31 | 12.8% | 20% | Juego, personajes, caballos reales (separación estricta canon/histórico), anime, manga, película, memes (incl. Mambo), estado 2026 |
| `ado` | 15 | 6.2% | 7% | Biografía, discografía, giras, colaboraciones, memes hispanos (Adominación, gyaru) |
| `cruzado` | 12 | 4.9% | 3% | Multi-hop entre dominios, desambiguaciones, verificación temporal, auditoría anti-rumor |

Los porcentajes de filas no son el objetivo; lo fue la distribución de **esfuerzo** (investigación + verificación + redacción). Miku recibió la mayor densidad de investigación (≈46 consultas web específicas) y sus filas son las más elaboradas.

## Esquema de cada fila

```json
{
  "id": "miku-0001",              // prefijo por dominio: miku-, ia-, uma-, ado-, cross-
  "domain": "hatsune_miku",       // hatsune_miku | ia_2024_2026 | uma_musume | ado | cruzado
  "subdomain": "historia",        // subárea temática
  "tags": ["lanzamiento", "2007"],// palabras clave
  "tipo": "factual",              // factual | multi_hop | temporal | comparativo |
                                  // desambiguacion | meme | canon_vs_fanon | conciencia_temporal
  "canon_o_fanon": "canon",       // canon | historico | fanon | meme | interpretacion | rumor | mixto
  "instruction": "¿...?",         // pregunta o consigna (español)
  "input": "",                    // contexto adicional (normalmente vacío)
  "output": "Respuesta...",       // respuesta densa y contextualizada (español,
                                  // conserva términos/títulos japoneses originales)
  "fecha_referencia": "2007-08-31", // fecha o año del hecho ("", rangos o años también)
  "confianza": "alta",            // alta | media | baja
  "fuente": "descripción breve",  // tipo de fuente usada en la verificación
  "idioma": "es",
  "corte": "2026-10-04"           // toda fila declara su fecha de corte
}
```

### Semántica de `canon_o_fanon`
- **canon** — hecho oficial/verificable dentro de la obra o industria.
- **historico** — hecho del mundo real (ej.: historias de los caballos reales de Uma Musume, fechas de lanzamiento).
- **fanon** — invención de la comunidad sin respaldo oficial.
- **meme** — fenómeno cultural comunitario (con origen y significado explicados en el `output`).
- **interpretacion** — lectura crítica/valoración argumentada, no hecho duro.
- **rumor** — circulante y no confirmado; siempre marcado y contextualizado (ej.: "face reveal" de Ado 2026).
- **mixto** — combina capas (p. ej. un fanloid semi-licenciado).

### Semántica de `confianza`
- **alta** — verificado por múltiples fuentes / fuente primaria / conocimiento estable desde hace años.
- **media** — verificado por una fuente web viva o reconstrucción razonable; detalles menores pueden variar.
- **baja** — señal explícita de "verificar antes de usar" (solo 1 fila, marcada adrede: face reveal de Ado).

## Metodología

1. **Investigación web en vivo (2026-10-05)**: ≈145 consultas de búsqueda distribuidas por dominio, con reintentos y verificación cruzada. Especialmente intensiva en: actualidad IA 2025-2026 (fuera del corte de entrenamiento de cualquier modelo), estado de los voicebanks de Miku (NT ver.2, V6), calendario de conciertos 2026 (Magical Mirai, Miku Expo Europa/NA), roster y hechos de Uma Musume (muertes de Haru Urara y Meisho Mambo, TGA 2025, versión global), y discografía/giras de Ado (Hibana, Vivarium).
2. **Regla de no invención**: si un dato no salió de fuentes verificables o conocimiento estable, o no se incluye, o se etiqueta `rumor`/`media`/`baja` con la incertidumbre explícita en el texto. Hay filas deliberadas de **anti-alucinación** (afirmaciones falsas famosas corregidas).
3. **Separación de capas**: historia real vs canon de obra vs fanon de comunidad, con etiquetas y ejemplos explícitos de confusión típica.
4. **Tipos difíciles**: ~24% de las filas son multi_hop, temporales, comparativas, de desambiguación, memes con origen o de conciencia temporal — no solo facts planos.

## Uso para fine-tuning

Formato instruction/input/output compatible con los scripts de SFT estándar (Alpaca-style). Ejemplo de conversión a chat:

```python
messages = [
  {"role": "user",      "content": row["instruction"] if not row["input"] else f"{row['input']}\n\n{row['instruction']}"},
  {"role": "assistant", "content": row["output"]},
]
```

Sugerencias:
- Filtra por `confianza` (`alta`/`media`) para el primer entrenamiento; usa `baja`/`rumor` para enseñar incertidumbre.
- Las filas `tipo=meme` y `canon_vs_fanon` están escritas con tono coloquial a propósito (petición explícita del proyecto): enseñan al modelo el registro del fandom.
- Las filas `corte=2026-10-04` de tipo `conciencia_temporal` ayudan al modelo a responder "¿qué pasa hoy?" sin inventar actualidad posterior.

## Estadísticas

- **243 filas**, ≈256 KB, 100% español.
- Tipos: factual 51.9%, temporal 19.8%, multi_hop 7.8%, meme 5.8%, comparativo 5.8%, conciencia_temporal 3.7%, desambiguacion 2.9%, canon_vs_fanon 2.5%.
- Canon: canon 87.7%, meme 5.8%, historico 3.3%, mixto 1.6%, fanon 0.8%, rumor 0.8%.
- Confianza: alta 61.7%, media 37.9%, baja 0.4%.
- Ver `dataset_stats.json` para el detalle completo.

## Limitaciones conocidas (honestidad ante todo)

- Las fechas de algunos conciertos de la gira **Miku Expo 2026 Europe** provienen de agregadores de ticketing y pueden moverse; confiança `media`.
- El listado exacto de G1 de Kitasan Black y algunos récords del turf se resumen; para apuestas/historia precisa, contrastar con netkeiba/JRA.
- Rumores de OPI/valoraciones de empresas IA en 2026 (Anthropic, OpenAI) son reportes de prensa, no cifras auditadas.
- El estado de lanzamiento exacto de Miku V6 a octubre de 2026 se declara según anuncios de early access (dic 2025) + plan H1 2026; verificar el sitio de Crypton antes de afirmar disponibilidad.

## Licencia

Los **hechos** pertenecen a sus fuentes (Crypton, SEGA, Cygames, Universal Music, laboratorios de IA, prensa). La **compilación, redacción y estructura** de este dataset se publica bajo **CC BY 4.0**. Los nombres de marcas y personajes son marcas de sus respectivos propietarios; este dataset es un trabajo de referencia educativa sin afiliación.

## Versionado

- **v1.0 (2026-10-05)**: 243 filas. Lanzamiento inicial con corte 2026-10-04.
- Roadmap sugerido: ampliar roster detallado de Uma Musume (una fila por uma con su caballo real), catálogo de canciones de Miku por era, y actualización mensual de la cronología IA.
