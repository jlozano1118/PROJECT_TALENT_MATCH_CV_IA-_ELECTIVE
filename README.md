# TalentMatch · CV Match 🎯

> **Conecta tu talento con los proyectos TI.** Plataforma interna que lee hojas de vida con IA, las convierte en un perfil JSON ATS y calcula en Python la compatibilidad de cada empleado con los roles abiertos en los proyectos de la empresa, incluyendo habilidades técnicas **y power skills**.

**Tercera iteración** · Electiva de programa *Problem Discovery & Solution Design with Artificial Intelligence* · Universidad Católica de Colombia · Octubre de 2026

---

## 👥 Integrantes

| Integrante |
|---|
| Juan Sebastián Lozano Calderón |
| Andrés Favid Rojas Villamil |
| Juan Sebastián López Urrego |
| Jeison Oswaldo Romero Cajamarca |

**Docente:** Juan Carlos Navarro Beltrán

---

## 🧩 ¿De qué trata el proyecto?

### El problema
Las empresas tienen empleados con experiencia y power skills que nadie ve a la hora de armar equipos. Los proyectos TI se asignan por intuición o contratando afuera, y las brechas aparecen cuando el proyecto ya arrancó.

### La solución
TalentMatch le permite al administrador de RR. HH. o a la PMO:

1. **Cargar una hoja de vida en PDF.**
2. Procesarla con **Claude Opus 5.5 API**, que extrae habilidades técnicas, power skills y experiencia.
3. Convertirla en un **JSON con formato ATS** (también disponible en Markdown).
4. Hacer el **matching en Python**: *oferta JSON vs. CV JSON*.
5. Obtener el **% de compatibilidad**, las **skills faltantes** (técnicas o power skills) y un **plan de cursos y certificaciones** con enlaces a Coursera, Udemy y Platzi.

Además muestra el **potencial de cada empleado en todos los puestos** de los proyectos de la empresa.

### ¿Por qué power skills?
Las power skills son la evolución de las soft skills: capacidades humanas, duraderas y transferibles que pueden entrenarse (González Pozo, 2026). Juliana González, de Blen360, nos recordó que son herramientas transversales que cambian con el tiempo gracias a la neuroplasticidad, y que el pensamiento crítico, la empatía y la comunicación son irreemplazables. Por eso TalentMatch las mide con un nivel de 0 a 100 en lugar de un sí o un no.

---

## 🔁 Flujo de la solución

```
CV PDF → Claude Opus 5.5 API → JSON ATS (técnicas + power skills + experiencia)
       → Python (match_engine.py): oferta JSON vs CV JSON
       → % de compatibilidad → skills faltantes → cursos / certificaciones
```

### Fórmula de compatibilidad

- **Skill técnica requerida:** `crédito = 0.6 × min(1, nivel / nivel_req) + 0.4 × min(1, años / años_req)`. Si la persona no tiene la skill, el crédito es 0.
- **Power skill requerida:** `crédito = min(1, nivel / nivel_req)`.
- **Match final:** `70 % × promedio técnico + 30 % × promedio power skills`.

| Rango | Nivel de potencial |
|---|---|
| ≥ 80 % | ✅ Listo para el rol |
| 60–79 % | 🟡 Con potencial |
| 40–59 % | 🟠 Requiere capacitación |
| < 40 % | 🔴 Brecha alta |

Los **años de experiencia por tecnología** salen de dos fuentes, y se toma la mayor: los años declarados en la skill y la suma de los periodos laborales donde se usó esa tecnología. Por ejemplo, si registras *Data Engineer 2022–2023 con Python y Apache Spark*, esas dos skills suman 1 año.

---

## 📈 Evolución por iteraciones

| Iteración | Origen | Qué se hizo |
|---|---|---|
| **01** | Prototipo en Figma | Carga de CV, extracción con Gemini API, % de encaje por proyecto, skills faltantes y cursos |
| **02** | Retroalimentación del grupo de Jurisprudencia | Página de bienvenida explicativa, edición del perfil extraído, brecha por nivel y años de experiencia |
| **03** | Esta versión | Pantalla de inicio animada, landing descriptiva, login de administrador, banco de CV, matriz de potencial empleado × puesto, power skills dentro del match, experiencia laboral editable, recomendaciones con enlaces y motor con Claude Opus 5.5 + Python |

---

## 🚀 Cómo usarlo

### Opción 1: abrirlo en tu computador
1. Descarga o clona el repositorio:
   ```bash
   git clone https://github.com/<tu-usuario>/cv-match.git
   cd cv-match
   ```
2. Abre `index.html` con doble clic. Funciona en Chrome, Edge o Firefox.
3. Se necesita internet para cargar las fuentes y la librería de gráficos (Chart.js).

> 💡 Para que la música cargue sin restricciones del navegador, sírvelo con un servidor local:
> ```bash
> python -m http.server 8000
> ```
> Luego abre `http://localhost:8000`.

### Opción 2: publicarlo con GitHub Pages
1. Sube `index.html` y `README.md` a la rama `main` del repositorio.
2. Ve a **Settings → Pages**.
3. En *Source* elige **Deploy from a branch**, luego `main` y `/ (root)`, y guarda.
4. En uno o dos minutos el sitio queda en `https://<tu-usuario>.github.io/cv-match/`.

### Recorrido de la demo
1. **Pantalla de inicio:** espera la carga y pulsa **▶ INICIAR**.
2. **Portada:** integrantes, para qué sirve, cómo funciona y gráficos interactivos. Haz clic en las barras y los segmentos.
3. **Comenzar análisis → Login.** Credenciales demo:
   - Correo: `admin.rrhh@novabanca.co`
   - Contraseña: `TalentMatch2026`
   - También puedes usar el botón *Autocompletar credenciales demo*.
4. **Banco de CV:** busca y filtra empleados. Abre uno para ver su radar de power skills, su experiencia y su ranking en todos los puestos.
5. **Analizar CV:** el flujo de 5 pasos.
   1. Carga un PDF o usa el CV de ejemplo.
   2. Mira el procesamiento con Claude Opus 5.5 y Python.
   3. Revisa el perfil extraído en JSON ATS o Markdown. Con **Editar perfil** puedes agregar skills, power skills y **experiencias** (cargo, empresa, años y tecnologías).
   4. Elige un rol y ve el % de compatibilidad con la brecha por nivel y años.
   5. Recibe el **plan de capacitación**: un diagnóstico del tipo *"le faltó saber sobre Linux"* y cursos con enlace directo.
6. **Proyectos:** roles abiertos con sus tres mejores candidatos.
7. **Matriz de potencial:** mapa de calor empleado × puesto. Haz clic en una celda para ver el análisis.
8. **Arquitectura:** el código `match_engine.py`, el prompt de extracción y la API propuesta.

### 🎵 Música de fondo ("Portals", Avengers: Endgame)
La canción tiene derechos de autor, por eso **no viene incluida** en el repositorio. Hay tres formas de hacerla sonar:

1. **En la pantalla de inicio:** pulsa **🎵 Cargar canción "Portals" (MP3)**, elige el archivo y luego **▶ INICIAR**.
2. **En cualquier momento:** usa el botón **Música** de la barra superior y *Cargar mi pista "Portals"*.
3. **Automática en tu computador:** crea la carpeta `assets/` junto a `index.html` y copia ahí el archivo con el nombre `portals.mp3`.

La página **recuerda la canción en tu navegador** (IndexedDB). Después de cargarla una vez, sonará sola al pulsar INICIAR en las siguientes visitas. El botón **Música** la pausa o la reanuda.

> ⚠️ Si el repositorio es público, **no subas el MP3**. Agrega esto a tu `.gitignore`:
> ```
> assets/*.mp3
> ```

---

## 🗂️ Estructura

```
cv-match/
├── index.html      # Sitio completo (HTML + CSS + JS en un solo archivo)
├── README.md       # Este documento
└── assets/         # (opcional, local) portals.mp3, no se sube si el repo es público
```

## 🛠️ Tecnologías
- HTML5, CSS3 y JavaScript sin frameworks
- [Chart.js 4.4.1](https://www.chartjs.org/) para los gráficos interactivos
- Web Audio API + IndexedDB para la banda sonora (se decodifica y se recuerda en el navegador)
- Lógica de matching equivalente a `match_engine.py` (Python 3.12)

## 🔮 Próxima iteración (04)
Backend con **FastAPI** conectado a los datasets `.csv` del equipo:

| Método | Endpoint | Función |
|---|---|---|
| POST | `/api/cv/parse` | PDF → Claude Opus 5.5 → JSON ATS |
| GET | `/api/empleados` | Lee `empleados.csv` |
| GET | `/api/proyectos` | Lee `proyectos.csv` y `roles.csv` |
| POST | `/api/match` | CV JSON vs. oferta JSON → % y brechas |
| GET | `/api/cursos?skill=` | Lee `cursos.csv` |

---

## ⚠️ Aviso
Todos los empleados, proyectos, empresas (NovaBanca), correos y cifras son **ficticios** y tienen fines académicos. La extracción con IA está **simulada** en esta iteración.

## 📚 Referencias (APA 7)

González Pozo, A. (2026, 25 de febrero). *Power skills: qué son, cuáles son las más demandadas y cómo desarrollarlas*. isEazy. https://www.iseazy.com/es/blog/power-skills/

Grupo de Jurisprudencia. (2026). *Retroalimentación de usabilidad del prototipo CV Match* [Evaluación no publicada]. Universidad Católica de Colombia.

Lozano Calderón, J. S., Rojas Villamil, A. F., López Urrego, J. S., y Romero Cajamarca, J. O. (2026). *CV Match: prototipo de hoja de vida* [Prototipo interactivo]. Figma. https://www.figma.com/make/X4BrLzRcwRFbpZESLq63D4/Prototipo-de-Hoja-de-Vida

*La comunicación personal con Juliana González (Blen360, 2026) se cita solo en el texto, según APA 7.*
# PROYECTO_IA_TALENTO_CV_MATCH
