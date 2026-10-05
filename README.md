# AI-ku_Knowledge

Dataset de conocimiento en formato **JSONL** (fine-tuning tipo SFT) en **español**, construido para el asistente **AI-ku**. Corte de conocimiento: **2026-10-04**. v1.0 compilado el 2026-10-05; **v2.0** amplía con cobertura general 2024→2026 (IA de frontera, hardware/infraestructura, agentes, ciencia y cultura) verificada con investigación web en vivo; **v2.1** completa la cultura 2025-2026, la ciencia pendiente y añade **Gemini 4 Argon** (30-sep-2026, limited preview); **v2.2** cierra los huecos de inventario de IA moderna 2024→2026 (Sonnet 4.6/5/5.5, Grok 4.5/4.7 y SpaceXAI, GPT-4o mini, Pulse, reorganización PBC, rondas Anthropic/OpenAI, Apple Intelligence, Alexa+, AMD/Intel/Maia, agentes OpenHands/Bolt/Lovable/Kiro, robótica humanoide, regulación SB 1047/53 y Take It Down) + cultura/españa/Nobel 2025; **v2.3** cierra el segundo barrido de cobertura (generadores de vídeo/imagen, agentes GitHub/Microsoft/Google, NVIDIA NVLink Fusion/B30A, herramientas OpenAI de nicho, TikTok-deal, H5N1-vacunas, orforglipron, BTS/BLACKPINK 2026); **v2.4** completa la cobertura 2024→corte (54 huecos: IA, ciencia/espacio, cultura/deporte/sociedad); **v2.5** añade los descubrimientos matemáticos/biológicos/materiales hechos por IAs (FunSearch, GNoME, AlphaProteo, AlphaChip, AI Scientist, AI co-scientist, GPT-4b micro, Equational Theories Project, rentosertib, cronología y récords), con separación explícita hecho/fanon.

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

Corte total v2.5: **560 filas** (+123 en v2.0, +50 en v2.1, +76 en v2.2, +20 en v2.3, +36 en v2.4, +12 en v2.5). El enfoque sigue la premisa CALIDAD > PROFUNDIDAD > COBERTURA > CANTIDAD: cada fila nueva está respaldada por fuentes específicas (ver `fuente`) y las afirmaciones no verificables se marcan `media`/`baja` o `rumor`.

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

## Estadísticas (v2.5)

- **560 filas**, ≈631 KB, 100% español.
- Por dominio: ia_2024_2026 42,5% (238), hatsune_miku 22,3% (125), cultura_2024_2026 13,4% (75), ciencia_2024_2026 9,5% (53), uma_musume 5,7% (32), cruzado 3,9% (22), ado 2,7% (15). Nota v2.5: cobertura 2024→corte COMPLETA desde v2.4; el reequilibrio Miku→40% requiere +157 filas (cálculo en roadmap v2.6).
- Tipos: factual 55,9%, temporal 20,9%, multi_hop 6,8%, comparativo 5,2%, meme 3,6%, canon_vs_fanon 3,6%, conciencia_temporal 2,9%, desambiguacion 1,2% → **~44% de filas no son facts planos**.
- Canon: canon 88,2%, historico 5,0%, meme 3,4%, mixto 2,7%, fanon 0,4%, rumor 0,4%.
- Confianza: alta 70,7%, media 28,9%, baja 0,4%.
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
- **v2.2 (2026-10-05)**: +76 filas tras auditoría de cobertura (inventario de 260 entidades → 99 huecos detectados). IA: GPT-4o mini, Pulse, chats grupales, voz Scarlett/Sky, rondas y valoraciones OpenAI ($6.6B→$40B→$500B) y reorganización PBC (28-oct-2025), Serie F Anthropic $13B (2-sep-2025), Microsoft-Nvidia-Anthropic (18-nov-2025), contratos DoD $200M (15-jul-2025), Anthropic↔Colossus de SpaceXAI (6-may-2026), Thinking Machines/SSI/Inflection/Character.ai/Broadcom-OpenAI, escala ChatGPT (900M WAU feb-2026), AI Overviews, NotebookLM, Jules, Gemma 2/4, SAM 2/3, Movie Gen, V-JEPA 2, DeepSeek V3.1-Terminus y -OCR, Kimi Linear, Qwen3-Coder/Omni, **Sonnet 4.6/5/5.5 (17-feb/30-jun/28-sep-2026)**, Cowork, Economic Index, Claude Plays Pokémon, **Grok 4.5 (9-jul-2026) y 4.7 (21-sep-2026) + SpaceXAI/Cursor**, AutoGLM/GLM-4.6 (chips domésticos), Seedream 4.0, UI-TARS, iFlytek X1 (Huawei), Yi-Lightning, MiniCPM, MAI, BitNet b1.58, Windows Recall, Alexa+, **Apple Intelligence (28-oct-2024)**, WWDC25/Siri-Gemini, Vision Pro/MLX, Cohere Command A/A+, Arctic/Jamba; hardware/agentes/regulación: AMD Instinct (MI300X→Helios), Gaudi 3/Falcon Shores, Maia 100, DLSS 4, Etched/Lightmatter/Tenstorrent, nuclear-TMI/Oklo, OpenHands, Replit Agent/Bolt.new, Lovable, Kiro/Firebase Studio→Antigravity, MLE-bench/Terminal-Bench, MLA/KV cache/especulativa, world models (Genie 3/Cosmos/V-JEPA 2), SB 1047/53, AI Diffusion Rule, Take It Down Act, humanoides (Unitree/Figure/GR00T/Optimus/1X). Cultura/ciencia: Eras Tour ($2.2B/149 shows), Sabrina Carpenter, Zootopia 2 (~$2.27B), Avatar: Fire and Ash (19-dic-2025), **DANA de Valencia (29-oct-2024)**, **apagón ibérico (28-abr-2025)**, Eurocopa 2024, **Nobel 2025 completos**, Stranger Things 5, aniversarios 18/19 de Miku, 1.º aniversario global de Umamusume. Metodología v2.2: `coverage_check.py` (matriz de entidades vs dataset) + Wikipedia action=raw (65 páginas nuevas, redirects resueltos) ante búsqueda 429.
- **v2.3 (2026-10-05)**: +20 filas tras el segundo barrido de cobertura (24 huecos detectados por `coverage_check.py`, 4 descartados por dedup semántico: Sora 2, Veo 3, chats grupales y estado Llama ya tenían fila). IA: vídeo generativo (Grok Imagine 4-ago-2025 con modo spicy y polémica de deepfakes, Hailuo/MiniMax con salida a bolsa HK ene-2026 y demanda de Hollywood sep-2025, Dream Machine jun-2024, Pika, comparativa de 6 sistemas al corte), imagen generativa (Ideogram 3.0, Recraft V3/red_panda oct-2024), agentes y productos (coding agent de GitHub 19-may-2025, Copilot Mode Edge jul-2025, Google Opal jul-2025), OpenAI de nicho (Aardvark oct-2025, benchmark BrowseComp abr-2025), NVIDIA (NVLink Fusion 18-may-2025 con Arm/SiFive/AWS Trainium4, B30A jul-2025), sesgos algorítmicos. Ciencia: H5N1 vacuna mRNA UK (BMJ 22-abr-2026), orforglipron→Foundayo FDA abr-2026 (1.er fármaco bajo National Priority Voucher). Cultura: **TikTok-deal cerrado 22-ene-2026** (Oracle/MGX/Silver Lake 15% c/u, ByteDance 19,9%), BTS en el 1.er halftime de la Final del Mundial 19-jul-2026 + 80M seguidores ×4 plataformas, BLACKPINK Guinness ICON 22-jun-2026 + 41,75B views YouTube. Metodología: Wikipedia action=raw (21 páginas + redirects resueltos) ante búsqueda 429 persistente; verificación de redirects (Dream Machine, MiniMax Group, Veo, H5N1) título a título.
- **v2.4 (2026-10-05)**: +36 filas cerrando la cobertura 2024→corte (matriz ampliada a ~310 entidades; ~54 huecos reales confirmados). IA/tech: 12 Días de OpenAI (dic-2024, o1-pro/Sora pública/Canvas/Tasks), Gemini dic-2024 (Flash Thinking, Veo 2, Whisk), vídeo/imagen abierta (HunyuanVideo, Wan 2.1, LTX-Video), Suno v4/v4.5/v5, World Labs/Marble, Adobe Firefly 3/4/video, apagón CrowdStrike (19-jul-2024), arresto de Durov (24-ago-2024). Ciencia/espacio: eclipse 8-abr-2024, fin de Ingenuity + Odysseus IM-1, reparación de Voyager 1 (abr-jun-2024), Europa Clipper (14-oct-2024), catch de Mechazilla (13-oct-2024), GenCast/WeatherNext. Cultura/sociedad/deporte: elecciones EE.UU. 2024 (312-226), DOGE, aranceles Liberation Day (2-abr-2025), caída de al-Ásad (8-dic-2024), condena SBF (25 años), Bitcoin 100K (dic-2024), París 2024 (Raygun, Marchand), **Milano-Cortina 2026 (Noruega 18 oros)**, retiro de Nadal (Davis Cup Málaga), Balón de Oro (Dembélé/Bonmatí), **PSG 5-0 Inter (31-may-2025)**, **F1: Norris campeón + McLaren constructores (2025)**, Pogačar (5 Tours hasta 2026 + Giro-Tour 2024), Dodgers bicampeón WS (2024-2025), Oasis Live '25, GNX de Kendrick, From Zero de Linkin Park, Eurovisión 2024-2026 (Nemo/JJ/Bulgaria), saga NewJeans/ADOR + regreso de G-Dragon, Wicked/For Good, Shōgun 18 Emmys + Arcane S2 + Fallout, Solo Leveling + Frieren T2. Metodología: 35 páginas Wikipedia nuevas (F1 2025, JJOO 2026, Eurovision 2026 verificados con fechas exactas de esta revisión).
- **v2.5 (2026-10-05)**: +12 filas de **descubrimientos hechos por IAs** (petición del usuario), todas verificadas con fuentes primarias ante búsqueda 429. Matemáticas: FunSearch (cap set 512 en dim. 8, dic-2023, histórico), Equational Theories Project de Tao (22.028.942 implicaciones cerradas en Lean, abr-2025; cita de o1 por Tao sep-2024), récords FunSearch→AlphaTensor→AlphaEvolve (48 productos 4x4, besos 11D 593, 75%/20% en 50 problemas). Biología/medicina: AlphaProteo (5-sep-2024, blog primario: 7 dianas, 3-300x afinidad), rentosertib de Insilico (USAN mar-2025, fase 2a en Nature Medicine, fase 3 a 2026, relojes de envejecimiento sep-2026), GPT-4b micro de OpenAI/Retro (17-ene-2025, MIT Tech Review, sin peer-review → confianza media), AI co-scientist (feb-2025). Materiales: GNoME (nov-2023, 736 validados por MIT + controversia Cheetham/Seshadri). Agentes/hardware: The AI Scientist de Sakana (ago-2024, ~$15/paper), AlphaChip (sep-2024 + crítica externa New Scientist/CACM). Además: fila canon_vs_fanon sobre Claude como descubridor (sin descubrimiento atribuido; instrumento en interpretabilidad mar-2025; fanon detectado) y cronología global 2023→2026. AlphaQubit descartada por falta de fuente primaria accesible. Roadmap v2.6 (cálculo de reequilibrio, ya hecho en Task 20): **+157 filas de Miku → 40% del total** (125→282 de ~705; la cuota IA baja a ~32,5%), o plan mínimo +80-105 para que Miku supere a IA. Opcional v2.7: +109 Uma y +34 Ado. Pendientes de cuota de búsqueda: capex/ingresos detallados y verificación primaria SpaceXAI-Cursor.
