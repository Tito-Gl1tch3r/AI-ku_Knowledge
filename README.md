# AI-ku_Knowledge

Dataset de conocimiento en formato **JSONL** (fine-tuning tipo SFT) en **español**, construido para el asistente **AI-ku**. Corte de conocimiento: **2026-10-04**. v1.0 compilado el 2026-10-05; **v2.0** amplía con cobertura general 2024→2026 (IA de frontera, hardware/infraestructura, agentes, ciencia y cultura) verificada con investigación web en vivo; **v2.1** completa la cultura 2025-2026, la ciencia pendiente y añade **Gemini 4 Argon** (30-sep-2026, limited preview).

## Dominios y prioridad

| Dominio | Filas (v1) | Filas añadidas v2.0 | Notas |
|---|---|---|---|
| `hatsune_miku` (ecosistema Vocaloid) | 124 | — (núcleo v1.0) | Historia, software/voicebanks, Crypton/Piapro/KARENT, conciertos, juegos, productores, canciones, memes, licencias, canon vs fanon |
| `ia_2024_2026` | 61 | **+43** | v2.0: OpenAI (GPT-5/5.1/5.2/5.6/6 Astra, Sora 2, Atlas, AgentKit, Stargate, OPI), Anthropic (Opus 4.5, Skills, acuerdo 1.5B$, Fable/Mythos), Google (Gemini 3, Antigravity, Nano Banana, Ironwood, Waymo), China (DeepSeek V4, Qwen3.x, Kimi K3, GLM-5.x, MiniMax), Meta TBD Lab, Mistral, xAI/Grok 5 (no verificado) |
| `ciencia_2024_2026` | 0 | **+24** | Nobel 2024/2025 (+calendario 2026), cuántica (Willow, Majorana 1, IBM Starling, NIST PQC, Quantum Echoes), fusión (NIF, EAST, ITER), cosmología (DESI, JWST, KM3NeT), espacio (Parker, Euclid, Rubin, 3I/ATLAS, Chang'e 6, Starship) |
| `cultura_2024_2026` | 0 | **+25 (v2.1) = 43** | Videojuegos (Switch 2 ventas, TGA 2025/Clair Obscur, GTA VI, BF6, MH Wilds, Steam Machine, Concord, Metroid Prime 4, Marvel Rivals, Palworld-patentes), cine/anime (Infinity Castle, KPop Demon Hunters, Dandadan, Óscar 2026, Emmy 2025), música (Showgirl, Bad Bunny Grammy AOTY, Kendrick), internet (Labubu, Italian brainrot, 6-7, Mangione, Diddy, Super Bowl LX) |
| `ia_2024_2026` hardware/agentes | (dentro del dominio IA) | **+28** | NVIDIA 5T$/Rubin, TPU v6/v7, NVFP4, vLLM/SGLang, llama.cpp/GGUF, superciclo HBM4/DRAM, MCP (adopción→AAIF), Claude Code/OpenCode/Cline/OpenClaw, Cursor/Windsurf/Devin, SWE-bench/METR/ARC-AGI-2/HLE, EU AI Act |
| `uma_musume` | 31 | — (núcleo v1.0) | Juego, personajes, caballos reales, anime, manga, memes |
| `ado` | 15 | — (núcleo v1.0) | Biografía, discografía, giras, memes |
| `cruzado` | 12 | **+10** | v2.0: multi-hop IA↔ciencia↔cultura, hecho vs mito (IMO, 3I/ATLAS, Nobel), cadenas Stargate→memoria→precios |

Corte total v2.1: **416 filas** (+123 en v2.0, +50 en v2.1). El enfoque sigue la premisa CALIDAD > PROFUNDIDAD > COBERTURA > CANTIDAD: cada fila nueva está respaldada por fuentes específicas (ver `fuente`) y las afirmaciones no verificables se marcan `media`/`baja` o `rumor`.

## Esquema de cada fila

```json
{
  "id": "miku-0001",              // prefijo por dominio: miku-, ia-, iah-, iaa-, ia2-, uma-, ado-, cross-, cie-, cul-, crx-
  "domain": "hatsune_miku",       // hatsune_miku | ia_2024_2026 | ciencia_2024_2026 | cultura_2024_2026 | uma_musume | ado | cruzado
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

1. **Investigación web en vivo (2026-10-05)**: v1.0 ≈145 consultas; **v2.0 añade ≈90 consultas** (IA/hardware/agentes 2025-2026, ciencia 2024-2026, cultura 2024-2026), con reintentos ante rate-limiting y verificación cruzada. Prioridad a fuentes primarias: blogs oficiales (OpenAI, Anthropic, Google, NobelPrize.org, NASA, ITER), papers (Nature, arXiv) y prensa técnica para el resto.
2. **Regla de no invención**: si un dato no salió de fuentes verificables o conocimiento estable, o no se incluye, o se etiqueta `rumor`/`media`/`baja` con la incertidumbre explícita en el texto. Ejemplos v2.0: Grok 5 (sin lanzamiento verificable al corte → `baja`), Teorías alienígena de 3I/ATLAS (`mixto`, desmentidas en el propio texto), Nobel 2026 (fila de conciencia temporal: "aún no anunciados").
3. **Separación de capas**: historia real vs canon de obra vs fanon de comunidad, con etiquetas y ejemplos explícitos de confusión típica.
4. **Tipos difíciles**: ~26% de las filas son multi_hop, temporales, comparativas, de desambiguación, memes con origen o de conciencia temporal — no solo facts planos.

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

## Estadísticas (v2.1)

- **416 filas**, ≈454 KB, 100% español.
- Por dominio: ia_2024_2026 33,7% (140), hatsune_miku 29,8% (124), cultura_2024_2026 10,3% (43), ciencia_2024_2026 9,9% (41), uma_musume 7,5% (31), cruzado 5,3% (22), ado 3,6% (15).
- Tipos: factual 51,9%, temporal 21,6%, multi_hop 8,2%, comparativo 5,0%, meme 4,6%, conciencia_temporal 3,8%, canon_vs_fanon 3,1%, desambiguacion 1,7% → **~48% de filas no son facts planos**.
- Canon: canon 85,3%, historico 6,2%, meme 4,3%, mixto 3,1%, fanon 0,5%, rumor 0,5%.
- Confianza: alta 67,1%, media 32,5%, baja 0,5%.
- Ver `dataset_stats.json` para el detalle completo.

## Limitaciones conocidas (honestidad ante todo)

- Las fechas de algunos conciertos de la gira **Miku Expo 2026 Europe** provienen de agregadores de ticketing y pueden moverse; confianza `media`.
- El listado exacto de G1 de Kitasan Black y algunos récords del turf se resumen; para apuestas/historia precisa, contrastar con netkeiba/JRA.
- Rumores de OPI/valoraciones de empresas IA en 2026 (Anthropic, OpenAI) son reportes de prensa, no cifras auditadas.
- **Grok 5**: no hay lanzamiento verificable al corte; la fila se limita a lo declarado públicamente (`baja`).
- **Familia GPT-5.6/GPT-6**: la nomenclatura Sol/Terra/Luna/Astra proviene de prensa técnica de jul-sep 2026; los detalles internos (tamaños) no son públicos.
- **Mythos 5.1 ≈ 8T parámetros** es estimación de prensa (FT), no cifras oficiales de Anthropic.
- El estado de lanzamiento exacto de Miku V6 a octubre de 2026 se declara según anuncios de early access (dic 2025) + plan H1 2026; verificar el sitio de Crypton antes de afirmar disponibilidad.
- **Gemini 4 Argon** está documentado en limited preview al corte (30-sep-2026): disponibilidad API amplia y precios finales ($4/$20 tras intro $2/$10) pueden moverse tras el corte.
- Ventas de consolas/juegos (Switch 2, BF6, Nightreign) son cifras vivas: se ancla la fecha de la cifra en cada fila.

## Licencia

Los **hechos** pertenecen a sus fuentes (Crypton, SEGA, Cygames, Universal Music, laboratorios de IA, prensa). La **compilación, redacción y estructura** de este dataset se publica bajo **CC BY 4.0**. Los nombres de marcas y personajes son marcas de sus respectivos propietarios; este dataset es un trabajo de referencia educativa sin afiliación.

## Versionado

- **v1.0 (2026-10-05)**: 243 filas. Lanzamiento inicial con corte 2026-10-04.
- **v2.0 (2026-10-05)**: +123 filas (IA de frontera 2024-2026, hardware/infra, agentes/MCP, ciencia, cultura 2024, cruzado). Nuevos dominios: `ciencia_2024_2026`, `cultura_2024_2026`. Corte sin cambios: 2026-10-04.
- **v2.1 (2026-10-05)**: +50 filas. **Gemini 4 Argon** (3 filas: modelo, precios/rollout Fairwind→API/AI Ultra, benchmarks DeepSWE/AutomationBench/Vals), familia Gemini 3.8 (Flash/Live/TTS/Cyber + Nano Banana 2 = 3.1 Flash Image), Neuralink, AlphaEvolve e IMO 2024/2025; ciencia completa (Polaris Dawn, Starliner, New Glenn, Artemis II — lanzada 1-abr-2026—, 2024 YR4, K2-18b, anti-amiloide, CRISPR KJ, conectoma FlyWire, mirror life, lobos de Colossal, mpox, H5N1, Acuerdo de Pandemia, récord térmico 2024, COP30, Fields 2026); cultura 2025-2026 (Switch 2, TGA 2025, GTA VI, Palworld-patentes, BF6, MH Wilds, Steam Machine, Concord, Infinity Castle, KPDH, Showgirl, Bad Bunny AOTY, Óscar/Emmy/Super Bowl LX, Labubu, brainrot, 6-7, Mangione, Diddy). Metodología v2.1: ante rate-limit persistente del buscador, verificación vía **Wikipedia (rev. 2026-10) + blog oficial de Google**, con fechas de revisión citadas en `fuente`.
- Roadmap v2.2: capex hiperescala 2026 desglosado, ingresos anualizados OpenAI/Anthropic con cifras auditables, acuerdo TikTok-EEUU ( Oracle/Silver Lake), comeback BTS 2026 y gira BLACKPINK (pendientes de verificación con cuota de búsqueda), GLP-1 orforglipron (detalles FDA), casos humanos H5N1 con fechas exactas.
