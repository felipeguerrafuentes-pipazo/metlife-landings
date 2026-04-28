# Landing Cliente MetLife

Proyecto de propuestas visuales para clientes MetLife Chile.
Asesor: Felipe Guerra · Código 35411051 · WhatsApp: 56935411051

---

## Workflow

1. Felipe hace R1 → escribe ficha en Notion
2. En claude.ai usa `/analisis-ficha-cliente-metlife` → sube cotizaciones PDF reales
3. Pega el output completo del análisis aquí → yo genero la landing

**Comando:** "genera la landing para [Nombre]" + pegar el output del análisis

---

## Input que recibiré (output de /analisis-ficha-cliente-metlife)

El análisis siempre llega en este orden. Saber de dónde sacar cada dato:

| Sección del análisis | Qué extraer para la landing |
|---------------------|----------------------------|
| 📋 Resumen ejecutivo | Nombre, edad, profesión, sueldo, urgencia, prima total |
| 🔍 Necesidades detectadas | Contenido de las 3 columnas del Diagnóstico |
| 📦 Plan recomendado | Qué productos incluir → qué secciones generar |
| 📊 Proyecciones 4A | Toggle A/B: primas, UF/mes, año 1/2/4/10, gráfico |
| 📊 Proyecciones 4B | Sección jubilación: barras AFP / AFP+APV op1 / op2 |
| 💰 APV Régimen A vs B | Sección APV: beneficio SII, ahorro anual |
| 📉 Costo de no hacer nada | Badge de urgencia en hero (edad actuarial, prima futura) |
| 🗣️ Scripts objeciones | NO va en la landing — es para Felipe |

---

## Productos → Secciones de la landing

| Producto en el análisis | Sección a generar |
|------------------------|-------------------|
| Salud Total | `#salud` — capital, prima familia, coberturas |
| Plan Integral (Vida+Ahorro) | `#integral` — toggle A/B, gráfico, tabla proyección |
| SVA (Seguro de Vida con Ahorro) | `#sva` cobertura + `#integral` proyección |
| APV | `#apv` — stat cards, régimen A vs B, proyección |
| Universitario Plus | `#universitario` — capital asegurado, edad hijo, meta |
| MetLife Joven | `#joven` — coberturas básicas, prima, edad límite |
| Cáncer 360 | Agregar a sección de salud como cobertura adicional |
| Accidental Full | Agregar a sección de protección como cobertura adicional |

**Regla:** Solo generar las secciones de los productos que aparecen en "Plan recomendado".

---

## Secciones fijas (siempre presentes)

1. **Nav** — links a las secciones activas + botón WhatsApp + toggle dark/light
2. **Hero** — nombre, edad, profesión, 4 stat cards, badge de urgencia si aplica
3. **Diagnóstico** — 3 columnas (lo que funciona / falta / meta) + frase de cierre
4. *(secciones de productos según plan)*
5. **Presupuesto** — desglose por producto, total, remanente sobre sueldo líquido
6. **CTA** — WhatsApp con mensaje pre-escrito para el cliente
7. **Footer** — legal + fecha

---

## Badge de urgencia en Hero

Mostrar si el análisis incluye en "Costo de no hacer nada":
- Edad actuarial próxima (< 6 meses para cumpleaños) → "Cumples X años el DD/MM — precio actual por N meses más"
- R2 con fecha urgente → mostrar fecha límite

---

## Diseño y stack

- **Archivos de referencia:** `clientes/hugo-irribarra/dark.html` (Salud + Integral + APV) y `clientes/adriana-rivera/dark.html` (SVA + APV)
- **Paleta dark:** fondo `#030D1A`, acento MetLife `#00A0DF`, texto `#F0F5FA`
- **Fuente números:** Georgia serif · **Fuente UI:** Inter
- **Toggle A/B** interactivo con Chart.js 4.4 y tabla de proyección
- **Light/dark mode** completo vía CSS variables
- **Sin dependencias** salvo Google Fonts + Chart.js CDN

---

## Datos numéricos clave

- **UF de referencia:** leer del análisis (campo "UF = $XX.XXX") — no asumir valor fijo
- **Rentabilidad proyectada:** 5% anual real (perfil Personalizado MetLife)
- **Proyecciones no garantizadas** — incluir siempre el disclaimer en footer

---

## Convenciones de formato numérico

- Pesos: `$164.118.900` (punto como separador de miles, estilo chileno)
- UF: `UF 4.100` o `UF 61,55` (punto para miles, coma para decimales)
- Porcentajes: `34%`

---

## Estructura de archivos

```
clientes/
  hugo-irribarra/dark.html   ← Salud Total + Plan Integral + Jubilación
  adriana-rivera/dark.html   ← SVA cobertura + Plan SVA ahorro + APV
template/landing.html        ← template light (versión anterior, no usar)
generar.py                   ← generador para template light (no usar)
CLAUDE.md                    ← este archivo
```

Nueva landing siempre en: `clientes/nombre-apellido/dark.html`
