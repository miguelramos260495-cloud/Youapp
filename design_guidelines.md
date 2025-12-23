# Diseño para "Sobre la Vía" - Aplicación de Navegación y Seguridad Vial

## Enfoque de Diseño

**Enfoque Seleccionado:** Híbrido - Utilidad optimizada para conducción con elementos visuales de seguridad

**Justificación:** Una app de navegación y seguridad vial requiere máxima legibilidad y accesibilidad mientras se conduce, combinada con señales visuales intuitivas de emergencia. Se inspira en patrones de apps de navegación (Google Maps, Waze) pero con énfasis en seguridad y asistencia.

**Principios Clave:**
- Interfaz oscura por defecto (reducir fatiga visual nocturna)
- Jerarquía visual clara mediante color de estado
- Botones grandes y táctiles para uso mientras se conduce
- Información crítica siempre visible
- Transiciones mínimas para rendimiento fluido

---

## Paleta de Colores

### Sistema de Estado por Color
**Rojo (Emergencia):** 0 85% 55% - Botón de pánico, alertas críticas, robo
**Naranja (Advertencia Legal):** 25 90% 55% - Asistencia legal, infracciones
**Amarillo (Precaución):** 45 95% 60% - Emergencias médicas, accidentes, alertas viales
**Verde (Vía Libre):** 145 70% 50% - Modo viaje seguro, confirmaciones, rutas despejadas

### Modo Oscuro (Principal)
**Fondo base:** 220 20% 12% (gris azulado muy oscuro)
**Fondo secundario:** 220 18% 18% (tarjetas, paneles)
**Fondo terciario:** 220 16% 24% (elementos elevados)
**Texto primario:** 0 0% 95%
**Texto secundario:** 0 0% 70%
**Bordes sutiles:** 220 15% 30%

### Acentos Funcionales
**Azul navegación:** 215 85% 55% - Enlaces, información de ruta
**Gris neutral:** 220 10% 50% - Elementos deshabilitados, información secundaria

---

## Tipografía

**Familia Principal:** Inter (Google Fonts) - Excelente legibilidad en pantallas y múltiples pesos
**Familia Secundaria:** Roboto Mono - Para datos numéricos (velocidad, distancia, coordenadas)

**Jerarquía:**
- **Títulos principales:** text-3xl font-bold (conductores), text-4xl font-bold (empresas/dashboard)
- **Subtítulos:** text-xl font-semibold
- **Cuerpo:** text-base font-normal
- **Botones principales:** text-lg font-semibold
- **Datos numéricos:** text-2xl font-mono font-bold (velocidad, distancia)
- **Información secundaria:** text-sm font-normal
- **Microtexto:** text-xs (timestamps, metadatos)

---

## Sistema de Espaciado

**Unidades Principales:** Usar múltiplos de 4 en Tailwind (4, 8, 12, 16, 20, 24, 32)

**Aplicación:**
- Padding de tarjetas: p-6 (móvil), p-8 (desktop)
- Separación entre secciones: space-y-8 (móvil), space-y-12 (desktop)
- Márgenes de contenedores: mx-4 (móvil), mx-auto max-w-7xl px-8 (desktop)
- Espaciado de botones: space-x-4 horizontal, space-y-4 vertical
- Grid gaps: gap-4 (tarjetas pequeñas), gap-6 (tarjetas medianas), gap-8 (secciones)

---

## Componentes Principales

### 1. Navegación
**Barra Superior Fija:**
- Logo a la izquierda (icono de carretera + escudo)
- Ubicación actual en el centro (icono + texto truncado)
- Menú hamburguesa a la derecha
- Altura: h-16, fondo: bg-[220 20% 12%] con backdrop-blur

**Navegación Móvil:**
- Drawer desde la izquierda, w-80
- Perfil del usuario arriba
- Items de menú con iconos grandes (h-12 w-12)
- Botón de cierre sesión al final

### 2. Botón de Pánico (Elemento Central)
**Diseño:**
- Botón circular grande: w-24 h-24 (móvil), w-32 h-32 (tablet+)
- Posición fija: fixed bottom-8 right-8, z-50
- Fondo con degradado según estado seleccionado
- Sombra pronunciada: shadow-2xl con resplandor del color activo
- Icono centrado: w-12 h-12
- Animación de pulso sutil en idle

**Estados del Botón:**
- Alerta Roja (presión simple): bg-gradient-to-br from-red-600 to-red-700
- Asistencia Legal (mantener 2-3s): bg-gradient-to-br from-orange-500 to-orange-600
- Emergencia Médica: bg-gradient-to-br from-yellow-500 to-yellow-600
- Modo Viaje Seguro: bg-gradient-to-br from-green-500 to-green-600

**Indicador de Presión:**
- Ring progress indicator alrededor del botón cuando se mantiene presionado
- Transición de 0 a 100% en 3 segundos

### 3. Mapa Principal
**Contenedor:**
- Ocupa h-[calc(100vh-4rem)] en vista de navegación
- Bordes redondeados: rounded-xl cuando está en contexto de pantalla (no fullscreen)
- Overlay de información en la parte inferior

**Controles del Mapa:**
- Botones de zoom: posición absolute top-4 right-4, vertical stack
- Botón de centrar ubicación: bottom-32 right-8
- Todos los controles: w-12 h-12, rounded-full, fondo semi-transparente bg-black/70 backdrop-blur-sm

**Overlay de Información:**
- Tarjeta deslizable desde abajo: max-h-[40vh]
- Muestra velocidad actual, límite de velocidad, tiempo estimado, distancia
- Números grandes en Roboto Mono
- Fondo: bg-[220 18% 18%]/95 backdrop-blur-md

### 4. Tarjetas de Alerta/Reportes
**Diseño:**
- Borde izquierdo grueso (border-l-4) del color según tipo
- Padding: p-4
- Fondo: bg-[220 18% 18%]
- Rounded: rounded-lg
- Icono grande a la izquierda (w-10 h-10)
- Título en font-semibold
- Timestamp en text-xs text-gray-400
- Sombra: shadow-md

### 5. Panel Empresarial
**Layout:**
- Sidebar izquierdo fijo: w-64, lista de conductores/vehículos
- Área principal: mapa o grid de tarjetas de estado
- Header con stats globales: grid-cols-4, mostrando total conductores, activos, alertas, distancia total

**Tarjetas de Conductor:**
- Grid responsive: grid-cols-1 md:grid-cols-2 lg:grid-cols-3
- Incluye: foto/avatar, nombre, vehículo, estado actual (con indicador de color), última ubicación
- Botón de "Ver en mapa" y "Contactar"

### 6. Bitácora de Viaje
**Vista de Lista:**
- Timeline vertical con conectores
- Cada entrada: tarjeta con hora inicio/fin, origen/destino, distancia recorrida, eventos destacados
- Iconos de eventos (infracciones, alertas, paradas) con su color correspondiente
- Expandible para ver detalles completos

**Vista Detalle:**
- Mapa de la ruta recorrida
- Métricas destacadas: duración, distancia, velocidad promedio/máxima
- Lista cronológica de eventos
- Galería de evidencias (fotos/videos) si las hay
- Botón de exportar (PDF/CSV)

### 7. Lugares de Servicio
**Cards de Lugares:**
- Imagen del lugar o icono grande según tipo
- Nombre y tipo (gasolinera, restaurante, hotel)
- Precio destacado (si aplica): text-2xl font-bold
- Servicios disponibles: chips pequeños (baño, wifi, comida, etc.)
- Distancia desde ubicación actual
- Calificación con estrellas
- Botón "Agregar a ruta"

### 8. Formularios
**Inputs:**
- Altura: h-12
- Padding: px-4
- Fondo: bg-[220 18% 18%]
- Borde: border border-[220 15% 30%]
- Focus: ring-2 ring-blue-500
- Texto: text-white
- Rounded: rounded-lg

**Botones Primarios:**
- Altura: h-12 (h-14 para acciones críticas)
- Padding: px-8
- Font: font-semibold text-lg
- Rounded: rounded-lg
- Según contexto: bg-blue-600 hover:bg-blue-700 (acciones normales)
- Acciones de emergencia: usar colores del sistema de estado

### 9. Sistema de Notificaciones/Toasts
**Posición:** fixed top-20 right-4
**Diseño:**
- Ancho: w-96 max-w-[calc(100vw-2rem)]
- Padding: p-4
- Fondo según tipo: éxito (verde), error (rojo), info (azul), advertencia (amarillo)
- Icono a la izquierda, texto, botón cerrar a la derecha
- Auto-dismiss en 5s (excepto emergencias)
- Entrada: slide-in desde derecha

---

## Animaciones

**Principio:** Animaciones mínimas y funcionales, sin distraer al conducir

**Aplicar solo en:**
- Transición de rutas/páginas: fade-in rápido (150ms)
- Botón de pánico: pulso sutil en estado activo
- Toasts: slide-in desde derecha
- Expansión de tarjetas: smooth expansion con duration-200
- Indicadores de carga: spinner simple

**Evitar:** parallax, scroll-driven animations, transiciones complejas

---

## Imágenes

### Logo
**Descripción:** Escudo estilizado con líneas de carretera atravesándolo, estilo moderno y minimalista
**Ubicación:** Navbar (h-10), splash screen (grande), favicon
**Formato:** SVG con versión en blanco para fondo oscuro

### Ilustraciones de Estado Vacío
**Ubicación:** Cuando no hay viajes en bitácora, no hay alertas, etc.
**Estilo:** Ilustraciones planas con los colores del sistema de estado
**Ejemplos:** Carretera vacía para "sin viajes", escudo para "sin alertas"

### Avatares de Usuario
**Tamaño:** w-10 h-10 (lista), w-20 h-20 (perfil), w-32 h-32 (detalle)
**Fallback:** Iniciales sobre fondo del color principal

### Íconos de Mapas
**Fuente:** Heroicons para UI general, iconos personalizados para tipos de vehículo y eventos específicos
**Tamaño:** w-5 h-5 (pequeños), w-6 h-6 (normales), w-10 h-10 (destacados)

---

## Responsividad

**Breakpoints Tailwind:**
- Mobile first: diseño base para sm (640px)
- md (768px): layout de 2 columnas donde aplique
- lg (1024px): dashboard completo, 3 columnas en grids
- xl (1280px): máxima densidad de información

**Componentes Adaptativos:**
- Mapa: fullscreen en móvil, 2/3 de pantalla en desktop
- Panel empresarial: sidebar oculto en móvil (drawer), visible en desktop
- Botón de pánico: más pequeño en móvil pero siempre accesible
- Tarjetas: stack vertical en móvil, grid en desktop

---

## Accesibilidad Específica para Conducción

- Contraste mínimo 4.5:1 en todos los textos
- Botones mínimo 44x44px (área táctil)
- Estados de foco claramente visibles
- Lecturas de pantalla para todas las alertas críticas
- Modo de alto contraste opcional
- Comandos de voz para funciones principales (próxima fase)
- Notificaciones con vibración y sonido distintivo según gravedad