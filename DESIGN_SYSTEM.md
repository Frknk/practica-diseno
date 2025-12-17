# Sistema de diseño de UtilesGo

Este documento resume las reglas visuales y los componentes disponibles en el proyecto para garantizar experiencias consistentes en todo el producto. Está dividido en fundamentos (color, tipografía, espaciado) y en la descripción detallada de cada componente junto con ejemplos de uso, estilos aplicados e indicaciones de reutilización.

## 1. Fundamentos visuales

### 1.1 Paleta y tokens
Los colores provienen de `src/routes/layout.css` y se exponen como variables CSS/Tailwind.

| Token | Valor (OKLCH) | Uso clave |
| --- | --- | --- |
| `--background` | `oklch(1 0 0)` | Fondo base en modo claro |
| `--foreground` | `oklch(0.129 0.042 264.695)` | Texto primario |
| `--card` / `--card-foreground` | `oklch(1 0 0)` / `oklch(0.129 0.042 264.695)` | Contenedores y textos dentro de tarjetas |
| `--primary` / `--primary-foreground` | `oklch(0.208 0.042 265.755)` / `oklch(0.984 0.003 247.858)` | Botones primarios, links destacados |
| `--secondary` | `oklch(0.968 0.007 247.896)` | Superficies neutras y badges secundarios |
| `--muted-foreground` | `oklch(0.554 0.046 257.417)` | Texto secundario / labels |
| `--accent` | `oklch(0.968 0.007 247.896)` | Hover states suaves |
| `--destructive` | `oklch(0.577 0.245 27.325)` | Estados de error |
| `--border` / `--input` | `oklch(0.929 0.013 255.508)` | Bordes y campos |

> **Modo oscuro:** se define en el mismo archivo utilizando la clase `dark`. Mantén los tokens cuando extiendas la paleta.

### 1.2 Tipografía
- Fuente base: la configuración global aplica clases Tailwind (`text-base`, `font-medium`) sobre `body`.
- Títulos: Ejemplos en `Header.svelte` (`text-3xl font-bold tracking-tight`) y `ProductCard.svelte` (`text-lg font-semibold`). Mantén jerarquía usando `text-3xl/2xl/lg` para títulos y `text-sm` para soporte.
- Colores: usa `text-foreground` para contenido principal y `text-muted-foreground` para contenido descriptivo.

### 1.3 Espaciado y radios
- Radio base: `--radius: 0.625rem`. Tarjetas y botones utilizan `rounded-md`/`rounded-xl`.
- Sistema de espaciado: Tailwind (`px-4`, `py-6`, `gap-6`). Para contenedores principales se usa `container mx-auto px-4`.

### 1.4 Iconografía
- Todos los iconos provienen de `lucide-svelte`. Mantén tamaños mediante utilidades (`class="size-4"`, `class="h-5 w-5"`).

## 2. Componentes atómicos

### 2.1 Button (`src/lib/components/ui/button/button.svelte`)
**Descripción:** botón interactivo con variantes y tamaños, compatible con `<button>` o `<a>`.

**Reglas de estilo:**
- Base: `inline-flex items-center gap-2 rounded-md text-sm font-medium transition-all`.
- Variantes (`buttonVariants`): `default`, `destructive`, `outline`, `secondary`, `ghost`, `link`.
- Tamaños: `default`, `sm`, `lg`, `icon`, `icon-sm`, `icon-lg`.
- Estados deshabilitados gestionados vía `disabled`/`aria-disabled`.

**Ejemplo de uso:**
```svelte
<script>
  import { Button } from "$lib/components/ui/button";
</script>

<Button variant="default">Comprar ahora</Button>
<Button variant="outline" size="lg" class="rounded-full">Descubrir</Button>
<Button variant="ghost" size="icon" aria-label="Abrir menú">
  <IconMenu />
</Button>
```

**Instrucciones de reutilización:**
1. Importa desde el barrel `"$lib/components/ui/button"` para obtener `Button` y los tipos de variantes.
2. Usa la prop `href` para renderizar un `<a>` con estilo de botón.
3. Extiende estilos con la prop `class` manteniendo la jerarquía (`class={cn(buttonVariants(...), "extra")}`).
4. Para nuevos patrones, añade variantes en `buttonVariants` y reexporta desde `index.ts` si es necesario.

### 2.2 Badge (`src/lib/components/ui/badge/badge.svelte`)
**Descripción:** etiqueta pequeña para estados o metadatos.

**Reglas de estilo:**
- Base: `inline-flex items-center rounded-full border px-2 py-0.5 text-xs font-medium`.
- Variantes: `default`, `secondary`, `destructive`, `outline`.

**Ejemplo:**
```svelte
<script>
  import { Badge } from "$lib/components/ui/badge";
</script>

<Badge>Nuevo</Badge>
<Badge variant="secondary">Borrador</Badge>
<Badge variant="destructive">Error</Badge>
```

**Reutilización:**
- Puede renderizar `span` o `a` dependiendo de si pasas `href`.
- Combina con íconos añadiéndolos como children.
- Extiende variantes en `badgeVariants` cuando necesites nuevas combinaciones de color.

### 2.3 Input (`src/lib/components/ui/input/input.svelte`)
**Descripción:** campo de formulario estándar compatible con la mayoría de `type`, con estilos consistentes.

**Reglas de estilo:**
- Altura: `h-9`, padding horizontal `px-3`.
- Estados focus: `focus-visible:ring-[3px]` + `border-ring`.
- Maneja el tipo `file` con un bloque específico (`pt-1.5`, `font-medium`).

**Ejemplo:**
```svelte
<script>
  import { Input } from "$lib/components/ui/input";
  let search = "";
</script>

<label class="flex flex-col gap-2">
  <span class="text-sm text-muted-foreground">Buscar producto</span>
  <Input type="search" bind:value={search} placeholder="Ingresa palabras clave" />
</label>
```

**Reutilización:**
1. Usa `bind:value` (o `bind:files` cuando `type="file"`).
2. Acepta atributos nativos (`min`, `max`, `required`).
3. Personaliza estilos con `class` pero evita eliminar los estilos base de accesibilidad.

## 3. Componentes de composición

### 3.1 Card System (`src/lib/components/ui/card/*`)
El conjunto de componentes permite estructuras modulares:
- `Card`: contenedor principal (`flex flex-col gap-6 rounded-xl border py-6`).
- `CardHeader`: grid adaptativo, soporta `CardAction` para acciones alineadas a la derecha.
- `CardTitle` y `CardDescription`: tipografía preconfigurada (`font-semibold`, `text-sm text-muted-foreground`).
- `CardContent`: wrapper con `px-6`.
- `CardFooter`: alineación horizontal (`flex items-center px-6`).
- `CardAction`: posicionamiento absoluto dentro del header (`col-start-2`).

**Ejemplo:**
```svelte
<script>
  import {
    Card,
    CardHeader,
    CardTitle,
    CardDescription,
    CardContent,
    CardFooter,
    CardAction
  } from "$lib/components/ui/card";
</script>

<Card>
  <CardHeader class="border-b">
    <div>
      <CardTitle>Plan Premium</CardTitle>
      <CardDescription>Para equipos de hasta 10 personas</CardDescription>
    </div>
    <CardAction>
      <Badge variant="secondary">Popular</Badge>
    </CardAction>
  </CardHeader>
  <CardContent class="space-y-4">
    <p>Incluye envíos express y soporte prioritario.</p>
    <ul class="list-disc pl-5 text-sm text-muted-foreground">
      <li>Catálogo completo</li>
      <li>Integraciones externas</li>
    </ul>
  </CardContent>
  <CardFooter class="border-t justify-between">
    <span class="text-2xl font-semibold">$49</span>
    <Button>Contratar</Button>
  </CardFooter>
</Card>
```

**Reutilización:**
- Combina sólo los subcomponentes necesarios; el orden no es estricto.
- Extiende `Card` para crear variantes (ej. `class="shadow-lg bg-primary text-white"`).
- Usa `data-slot` para tests o estilos específicos.

## 4. Componentes aplicados a página

### 4.1 Header (`src/lib/components/Header.svelte`)
**Descripción:** barra superior con navegación, búsqueda y CTA.

**Estructura:**
- Contenedor `header.border-b.py-4` + `container mx-auto flex items-center justify-between px-4`.
- Logo (texto) enlazado a `/`.
- Navegación secundaria (links con `hover:text-primary`). Se oculta en mobile (`hidden md:flex`).
- Área de acciones: buscador (`Input` + icono `Search`) visible a partir de `sm`, y botón `Login` (`Button variant="default"`).

**Ejemplo de integración:**
```svelte
<script>
  import Header from "$lib/components/Header.svelte";
</script>

<Header />
```

**Reutilización:**
1. Cambia destinos de navegación actualizando los `<a>` internos.
2. Ajusta la acción principal reemplazando el contenido del contenedor `Actions` (por ejemplo, añadir un botón de registro).
3. El buscador usa `Input` con `type="search"`; puedes exponer `bind:value` agregando props al componente si necesitas levantar el estado.

### 4.2 ProductCard (`src/lib/components/ProductCard.svelte`)
**Descripción:** tarjeta promocional para mostrar un producto destacado.

**Props disponibles:**
- `title`: nombre del producto (string).
- `type`: categoría/descriptor (string).
- `badge`: texto opcional para `Badge` (ej. “Nuevo”).
- `imageColor`: fondo de la imagen (`bg-gray-200` por defecto).
- `rating`: número mostrado junto al ícono `Star` (4.5 por defecto).

**Estilos clave:**
- Usa el sistema de tarjetas (`Card`, `CardHeader`, etc.) para heredar espaciado.
- Imagen compuesta con `aspect-square w-full ... rounded-xl`.
- Botón `variant="outline"` con esquinas redondeadas (`rounded-full`).

**Ejemplo:**
```svelte
<script>
  import ProductCard from "$lib/components/ProductCard.svelte";
</script>

<ProductCard
  title="Pack Escolar Creativo"
  type="Útiles + Arte"
  badge="-15%"
  imageColor="bg-pink-100"
  rating={4.8}
/>
```

**Reutilización:**
1. Separa logotipos o imágenes reemplazando el icono `Image` dentro del componente (puedes pasar un slot si decides extenderlo).
2. Cambia la llamada a la acción editando el `Button` del footer (p.ej. `variant="default"`).
3. Combínalo dentro de un grid (`grid-cols-2 md:grid-cols-4 gap-6`) para listados.

## 5. Instrucciones generales de reutilización

1. **Importaciones centralizadas:** usa los barrels (`$lib/components/ui/button`, `$lib/components/ui/card`, etc.) para mantener las rutas cortas y beneficiarte de posibles utilidades compartidas (`cn`, `WithElementRef`).
2. **Tailwind + tokens:** siempre que personalices estilos, usa las variables (`text-primary`, `bg-card`, `border-border`) para no romper el modo oscuro y mantener consistencia.
3. **Accesibilidad:**
   - Conserva atributos `aria-` y estados `focus-visible` que vienen en los componentes base.
   - Para botones que actúan como enlaces, usa la prop `href` en `Button` en lugar de aplicar clases manualmente.
4. **Composición:** los componentes están pensados para usarse juntos (e.g. `ProductCard` combina `Badge`, `Button`, `Card`). Antes de crear un componente nuevo, verifica si puedes extender los existentes con props o `class`.
5. **Testing/QA:** cada componente UI define `data-slot` (ej. `data-slot="button"`). Úsalos para selectores estables en pruebas end-to-end.

Con estas pautas puedes extender la biblioteca de componentes manteniendo alineación visual y funcional en toda la aplicación UtilesGo.

## 6. Patrones de página y flujos clave

Los siguientes patrones se basan en los archivos de `src/routes` y describen cómo ensamblar los componentes UI para lograr experiencias completas.

### 6.1 Lista de productos destacada (`src/routes/+page.svelte`)
**Descripción:** página inicial que muestra una cuadrícula de productos destacados usando `ProductCard`. Úsala cuando necesites un catálogo resumido con CTA hacia detalles o compra.

**Reglas de estilo:**
- Contenedor general: `div.min-h-screen bg-white font-sans` para mantener contraste en modo claro.
- `Header` fijo al tope seguido de `<main class="container mx-auto px-4 py-12">` para alinear el contenido con el grid.
- Hero textual centrado (`text-center`, `text-3xl font-bold`, `text-muted-foreground`) para titular + subtítulo.
- Grid responsive: `grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-8`; controla densidad entre breakpoints.

**Ejemplo de uso:**
```svelte
<script>
  import Header from "$lib/components/Header.svelte";
  import ProductCard from "$lib/components/ProductCard.svelte";

  const products = [
    { title: "Mochila Escolar", type: "Mochilas", badge: "Nuevo", imageColor: "bg-blue-100", rating: 4.8 },
    { title: "Set de Lápices", type: "Lápices", badge: "Oferta", imageColor: "bg-yellow-100", rating: 4.5 }
  ];
</script>

<div class="min-h-screen bg-white">
  <Header />
  <main class="container mx-auto px-4 py-12">
    <div class="mb-10 text-center">
      <h2 class="text-3xl font-bold tracking-tight mb-2">Productos Destacados</h2>
      <p class="text-muted-foreground">Encuentra los mejores útiles</p>
    </div>
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
      {#each products as product}
        <ProductCard {...product} />
      {/each}
    </div>
  </main>
</div>
```

**Reutilización:**
1. El listado se basa en un arreglo de objetos plano; agrega filtros o paginación envolviendo la grilla en un `section` con controles.
2. Cambia el layout modificando las utilidades del grid (por ejemplo, `md:grid-cols-2` para tablets).
3. Para destacar campañas, intercambia el texto del hero y añade `Badge` o `Button` dentro del bloque central.

### 6.2 Pantalla de inicio de sesión (`src/routes/login/+page.svelte`)
**Descripción:** formulario centrado para autenticación institucional. Combina `Header`, `Card`, `Input` y `Button` para ofrecer una experiencia clara.

**Reglas de estilo:**
- Layout principal: `flex flex-col` con `main` en `flex-1` para centrar el formulario verticalmente.
- Diseño responsive de dos columnas (`grid grid-cols-1 md:grid-cols-2 gap-12`): imagen ilustrativa izquierda (oculta en móviles) y formulario a la derecha.
- Formulario dentro de `Card.Root` sin sombras (`border-none shadow-none`) y contenido apilado (`space-y-6`).
- Inputs etiquetados con `label.text-sm font-medium` y placeholders neutrales.
- Botón primario personalizado: `class="w-full bg-neutral-800 hover:bg-neutral-900 text-white" size="lg"` para contraste.

**Ejemplo:**
```svelte
<script>
  import Header from "$lib/components/Header.svelte";
  import { Button } from "$lib/components/ui/button";
  import { Input } from "$lib/components/ui/input";
  import * as Card from "$lib/components/ui/card";
  import { Image } from "lucide-svelte";
</script>

<div class="min-h-screen bg-white flex flex-col">
  <Header />
  <main class="flex-1 container mx-auto px-4 py-12 flex items-center justify-center">
    <div class="w-full max-w-6xl grid grid-cols-1 md:grid-cols-2 gap-12 items-center">
      <div class="hidden md:flex flex-col gap-4">
        <h2 class="text-3xl font-bold tracking-tight">Marketplace</h2>
        <div class="aspect-square bg-gray-200 rounded-lg flex items-center justify-center">
          <Image class="w-32 h-32 text-gray-300" />
        </div>
      </div>
      <div class="w-full max-w-md mx-auto">
        <Card.Root class="w-full border-none shadow-none">
          <Card.Content class="space-y-6 p-0">
            <label class="space-y-2">
              <span class="text-sm font-medium">Correo institucional</span>
              <Input type="email" placeholder="nombre@colegio.edu" />
            </label>
            <label class="space-y-2">
              <span class="text-sm font-medium">Contraseña</span>
              <Input type="password" placeholder="••••••••" />
            </label>
            <Button class="w-full bg-neutral-800 hover:bg-neutral-900 text-white" size="lg">
              Inicio de Sesión
            </Button>
          </Card.Content>
          <Card.Footer class="justify-center p-0 mt-6">
            <p class="text-sm text-muted-foreground">
              ¿No tienes cuenta? <a href="/register" class="underline">Regístrate</a>
            </p>
          </Card.Footer>
        </Card.Root>
      </div>
    </div>
  </main>
</div>
```

**Reutilización:**
1. Para flujos de registro, reutiliza la estructura del formulario y cambia el texto principal + campos requeridos.
2. Integra validaciones añadiendo props `aria-invalid` o mensajes debajo de cada `Input` manteniendo `text-sm text-destructive`.
3. Si necesitas autenticación social, agrega un `div` con botones secundarios dentro de `Card.Content` conservando el `space-y-6`.

### 6.3 Detalle de producto e intercambio (`src/routes/product/+page.svelte`)
**Descripción:** página de detalle con columnas para imagen, especificaciones, vendedor y chat seguro para concretar el intercambio/compra.

**Reglas de estilo:**
- Grid de tres columnas (`grid-cols-1 md:grid-cols-3 gap-8`) adaptado a móviles (se apila verticalmente).
- Identidad visual tipo editorial: bordes dobles (`border-2 border-neutral-950`), fondos blancos y tipografías en mayúsculas.
- Columna izquierda: imagen cuadrada con "placeholder" en X, sección de tipos de contacto y botón `Button variant="outline"` sin borde superior.
- Columna central: tarjetas `Card` sin sombra para detalles (`CardTitle text-2xl`, `CardContent text-lg`), tarjeta de autor y un placeholder para galería.
- Columna derecha: contenedor de chat con header, mensajes, y footer compuesto por `Input` + botones icono.

**Ejemplo:**
```svelte
<script>
  import Header from "$lib/components/Header.svelte";
  import { Button } from "$lib/components/ui/button";
  import { Card, CardContent, CardHeader, CardTitle } from "$lib/components/ui/card";
  import { Input } from "$lib/components/ui/input";
  import { User, Clock, MessageCircle, Check, Smile, Send, Mic } from "lucide-svelte";
</script>

<div class="min-h-screen bg-white">
  <Header />
  <main class="container mx-auto px-4 py-8">
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
      <!-- Imagen y acciones -->
      <section class="flex flex-col gap-6 border-2 border-neutral-950 p-6">
        <!-- Imagen placeholder -->
        <div class="border-2 border-neutral-950">
          <div class="aspect-square bg-gray-50 relative border-b-2 border-neutral-950">
            <!-- líneas en X -->
          </div>
          <div class="p-4 text-center">
            <h2 class="text-2xl font-bold uppercase tracking-wider">Intercambio</h2>
          </div>
        </div>
        <!-- Tipos de contacto -->
        <div class="border-2 border-neutral-950 p-4">
          <h3 class="font-medium mb-4">Tipo de contactos</h3>
          <div class="flex gap-6">
            <MessageCircle />
            <MessageCircle />
            <MessageCircle />
          </div>
        </div>
        <Button class="w-full h-12 text-lg rounded-none" variant="outline">Iniciar chat en línea</Button>
      </section>

      <!-- Detalles del producto -->
      <section class="flex flex-col gap-6 border-2 border-neutral-950 p-6">
        <Card class="border-2 border-neutral-950 rounded-none shadow-none">
          <CardHeader>
            <CardTitle class="text-2xl font-bold">Detalles</CardTitle>
          </CardHeader>
          <CardContent class="space-y-4 text-lg">
            <p>Camisa color blanco</p>
            <p><span class="font-semibold">Marca:</span> Gucci</p>
            <p><span class="font-semibold">Talla:</span> S</p>
          </CardContent>
        </Card>
        <Card class="border-2 border-neutral-950 rounded-none shadow-none flex items-center gap-4 p-4">
          <div class="h-10 w-10 rounded-full border-2 border-neutral-950 flex items-center justify-center">
            <User />
          </div>
          <span class="text-xl font-bold">Fred Polinar</span>
        </Card>
      </section>

      <!-- Chat seguro -->
      <section class="border-2 border-neutral-950 flex flex-col h-[800px] p-4 gap-4">
        <header class="border-2 border-neutral-950 p-3 flex items-center justify-between text-sm font-medium">
          <div class="flex items-center gap-4">
            <Clock class="h-4 w-4" />
            <span>20 Minutos</span>
          </div>
          <div class="flex items-center gap-2">
            <span>En línea</span>
            <div class="h-3 w-3 rounded-full bg-green-500 border border-neutral-950"></div>
          </div>
        </header>
        <div class="flex-1 border-2 border-neutral-950 p-4 space-y-8 overflow-y-auto">
          <!-- Mensajes -->
          <div class="space-y-2">
            <div class="text-xs text-muted-foreground flex items-center gap-2">
              <Clock class="h-3 w-3" /> Hace 2 min
            </div>
            <div class="border-2 border-neutral-950 p-3">
              Hola, ¿sigue disponible?
            </div>
          </div>
        </div>
        <footer class="border-2 border-neutral-950 p-4 space-y-2">
          <div class="flex items-center justify-center gap-2 text-xs">
            <span>Este chat es seguro</span>
            <Mic class="h-4 w-4" />
          </div>
          <div class="relative">
            <Input class="border-2 border-neutral-950 rounded-none h-12 pr-20" placeholder="Escribe un mensaje" />
            <div class="absolute right-2 top-1/2 -translate-y-1/2 flex gap-2">
              <Button variant="ghost" size="icon"><Smile /></Button>
              <Button variant="ghost" size="icon"><Send /></Button>
            </div>
          </div>
        </footer>
      </section>
    </div>
  </main>
</div>
```

**Reutilización:**
1. La estructura de tres columnas puede adaptarse a otros verticales (por ejemplo, venta directa) cambiando el contenido del `Card` central.
2. Para compras tradicionales reemplaza el botón “Iniciar chat” por `Button variant="default"` + acciones de compra (añadir al carrito, comprar ahora).
3. El módulo de chat puede extraerse a un componente independiente reutilizable; asegúrate de mantener los estilos de bordes dobles para preservar la estética.
