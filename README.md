# jarvis

Asistente sencillo para Windows en Python. Funciona por texto o por voz.

## Instalación (PowerShell)

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Si PowerShell bloquea la activación: `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`.

Si `PyAudio` falla al instalar, usa solo el modo texto (`--mute` o sin `--voz`) o prueba `pip install pipwin` y luego `pipwin install pyaudio`.

## Uso

```powershell
python jarvis.py          # modo texto
python jarvis.py --voz    # modo voz: di "Jarvis, qué hora es"
python jarvis.py --mute   # sin voz de respuesta
```

## Comandos

- `qué hora es`, `qué fecha es`
- `abre calculadora`, `abre bloc de notas`, `abre chrome`...
- `busca recetas de arroz` (Google), `youtube música relajante`
- `anota comprar leche` (guarda en `notas.txt`)
- `ayuda`, `salir`

## Respuestas con IA (opcional)

Para que Jarvis responda preguntas generales, define tu clave de API de Anthropic antes de ejecutarlo:

```powershell
$env:ANTHROPIC_API_KEY = "tu-clave"
python jarvis.py
```

Sin clave, solo funcionan los comandos locales.

## Voz de ElevenLabs (Melody)

Jarvis usa la voz **Melody** de ElevenLabs (ID `MYRJe6h0let7Xxh9zMPi`) cuando defines tu clave de API:

```powershell
$env:ELEVENLABS_API_KEY = "tu-clave-de-elevenlabs"
python jarvis.py
```

Notas:
- La clave se crea en elevenlabs.io (Developers > API Keys).
- Melody es una voz de la biblioteca pública: agrégala primero a "My Voices" en tu cuenta (botón "Use voice" en su página). Según el plan de tu cuenta, ElevenLabs puede limitar el uso de voces de la biblioteca por API; si da error, Jarvis lo muestra y usa la voz de Windows.
- Cada respuesta hablada consume caracteres de tu cuota de ElevenLabs.
- Opcional: `$env:ELEVENLABS_MODEL = "otro_model_id"` para cambiar el modelo (por defecto `eleven_multilingual_v2`).

## Privacidad

En modo voz, el audio se envía al servicio de reconocimiento de Google para convertirlo en texto. Con la IA activada, tus preguntas se envían a la API de Anthropic, y con ElevenLabs activo, el texto de cada respuesta se envía a ElevenLabs.
