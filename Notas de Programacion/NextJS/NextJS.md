Next.js es un framework de React que permite crear aplicaciones web rápidas y eficientes con *server-side rendering* y *static site generation.*

**Server-Side Rendering (SSR):** es cuando las páginas web se generan en el servidor cada vez que se solicita una, enviando al navegador una página completamente renderizada.

**Static Site Generation (SSG):** es cuando las paginas web se generan en build-time, creando archivo HTML estáticos que se sirven al usuario, lo que hace que las páginas sean rápidas y fáciles de alojar.

## Estructura de Carpetas:

- `/app`: contiene todas las rutas, componentes y logica de la app.
- `/app/lib`: contiene funciones de utilidad reutilizables y funciones de fetching de datos.
- `/app/ui`: contiene todos los componentes de UI de la app. En el tutorial, estos componentes ya vienen con estilos para ahorrar tiempo.
- `/public`: contiene los assets estaticos de la app, como imagenes.
- **Archivos de Configuración:** la mayoría de estos archivos se crean y se preconfiguran al crear un nuevo proyecto con `create-next-app`. Por ej.: el archivo `next.config.mjs`

`create-next-app` es un CLI que configura la app de Next.js

## Estilos:

Se usa el fichero `global.css` para agregar estilos globales, este fichero se puede importar en cualquier componente pero es buena practica tenerlo en el top-level, en el `/app/layout.tsx`

Para estilar también se puede usar `Tailwindcss`. Al correr el comando `create-next-app` para iniciar un nuevo proyecto, Next.js preguntará si se quiere usar tailwind. Si se selecciona que *sí,* Next.js va a configurar e instalar los paquetes necesarios para usar en la app.

También se puede usar `CSS` de forma tradicional y `CSS Modules`.

```tsx
import styles from '@/app/ui/home.module.css';
 
export default function Page() {
  return (
    <main className="flex min-h-screen flex-col p-6">
      <div className={styles.shape} />
    // ...
  )
}
```

`Tailwindcss` y `CSS modules` son las formas más comunes de estilar apps en Next.js.

`clsx` es una librería que permite altenar classnames de forma facil, puede servir para agregar estilos basados en el estado o en una condición:[https://github.com/lukeed/clsx](https://github.com/lukeed/clsx)

```tsx
import clsx from 'clsx'; 

export default function InvoiceStatus({ status }: { status: string }) {
  return (
    <span
      className={clsx(
        'inline-flex items-center rounded-full px-2 py-1 text-sm',
        {
          'bg-gray-100 text-gray-500': status === 'pending',
          'bg-green-500 text-white': status === 'paid',
        },
      )}
    >
    // ...
)}
```

Otras alternativas pueden ser: `SASS`, librerías CSS-in-JS como `styled-jsx`, `styled-components` y `emotion`.

## Optimización de fuentes:

Las fuentes pueden afectar al rendimiento si estan en una carpeta y tienen que ser cargadas o obtenidas.

Next.js optimiza automaticamente las fuentes cuando se usa el modulo `next/font`. 

Descarga las fuentes en build-time y las aloja con los otros assets estáticos. Esto significa que cuando el usuario entre la app, no se hará solicitudes adicionales para la fuente, evitando así el *Flash of Unstyled Text* o *Flash of Invisible Text*.

```tsx
// archivo `fonts.ts`
import { Inter } from 'next/font/google';

// se especifica el subset, en este caso 'latin' 
export const inter = Inter({ subsets: ['latin'] }); 
```

Luego se importa y se usa en el elemento `<body>` en `/app/layout.tsx`:

```tsx
import '@/app/ui/global.css';
import { inter } from '@/app/ui/fonts';
 
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className={`${inter.className} antialiased`}>{children}</body>
    </html>
  );
}
```

Añandiendo `Inter` en el elemento `<body>`, la fuente se aplicará en toda la app. Ahí también se agrega la clase `antialiased` que suaviza la fuente, no es necesario pero es un poco más agradable.

## Optimizacion de Imagenes:

Los archivos de la carpeta `/public` pueden ser referenciados en cualquier parte de la app.

Con HTML regular, agregar una imagen se haría así:

```html
<img
	src="/hero.png"
	alt="Screenshots of the dashboard project showing desktop version"
/>
```

Esto significa hacer manualmente:

- Que la imagen sea responsiva.
- Especificar el tamaño de la imgen en diferentes dispositvos.
- Prevenir el layout shift mietras que se cargue la imagen.
- Lazy load de las imagenes que estan fuera del viewport del user.

En vez de hacer todo esto manualmente se puede usar el componente `next/image` para optimizar las imagenes de forma automática.

El componente `<Image>` es una estensión de la etiqueta `<img>` de HTML y viene con algunas optimizaciones automáticas como:

- Previene el layout shift cuando se cargan las imagenes.
- Cambia el tamaño de la imagen para evitar enviar imagenes grandes a dispositivos pequeños.
- Lazy load por defoult (las imagenes se cargan solo cuando entran en el viewport).
- Sirve las imagenes en formato WebP o AVIF cuando el navegador lo soporta.

```tsx
// otros imports
import Image from 'next/image'; 

export default function Page() {
  return (
    // ...
    <div className="flex items-center justify-center p-6 md:w-3/5 md:px-28 md:py-12">
      {/* Se usa acá */}
      <Image
        src="/hero-desktop.png"
        width={1000}
        height={760}
        className="hidden md:block"
        alt="Screenshots of the dashboard project showing desktop version"
      />
    </div>
    //...
  );
}
```

Es buena practica agregar el `width` y el `height` para evitar el layout shift, debe tener el aspect ratio identico a la imagen orignal.

## Layouts and Pages

### Rutas anidadas

Next.js para las rutas usa el *file-systema routing* para crear rutas anidadas. Cada carpeta representa un segmento de ruta que se asigna a un segmento de la URL.

Se puede crear UIs separada para cada ruta usando los archivos `layout.tsx` y `page.tsx`.

`page.tsx` es un archivo especial de Next.js que exporta un componente de React y es requerido para que la ruta sea accesible. En las apps creadas con Next.js ya se tiene el archivo `/app/page.tsx`, esta es la home page asociada a la ruta `/`.

Para crear rutas anidadas, se puede anidar carpetas y dentro de cada una agregar el achivo `page.tsx`. Por ejemplo: `/app/dashboard/page.tsx` esta asociado a la ruta `/dashboard`.

```tsx
export default function DashboardPage() {
  return <p>Dashboard Page</p>;
}
```

Es un buena practica poner nombres descriptivos.

Al tener el nombre de archivo especial `page`, Next.js permite colocar componentes de UI, los tests y otros archivos y carpetas relacionadas con las rutas. Solo el contenido dentro del archivo `page` sera accesible publicamente. 

### Layouts:

En Next.js se puede usar el archivo especial `layout.tsx` para crear interfaces que estan compartidas entre multiples las multiples páginas.

Por ejemplo en este proyecto se creará un archivo `layout.tsx` dentro de la carpeta `/dasboard`:

```tsx
import SideNav from '@/app/ui/dashboard/sidenav';
 
export default function DashboardLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="flex h-screen flex-col md:flex-row md:overflow-hidden">
      <div className="w-full flex-none md:w-64">
        <SideNav />
      </div>
      <div className="flex-grow p-6 md:overflow-y-auto md:p-12">{children}</div>
    </div>
  );
}
```

Acá se importa el componente `<SideNav />` en el layout, cualquier componente que se importe dentro de este archivo será parte del layout.

El componene `<Layout />` recibe una prop `children`. Este hijo puede ser cualquier página o otro layout, en el caso del proyecto del tutorial, cualquier página dentro de `/dasboard` sera anidada automaticamente dentro del componente `<Layout />`. Este layout es unicamente para las páginas del dashboard.

Uno de los beneficios de usar layouts en Next.js es en la navegación, porque solo los componentes de la página se actualizarán, mientras que el layout no se re-renderiza. Esto se llama *renderizado parcial*.

### RoutLayout:

```tsx
import '@/app/ui/global.css';
import { inter } from '@/app/ui/fonts';
 
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className={`${inter.className} antialiased`}>{children}</body>
    </html>
  );
}
```

Esto se llama root layout y es necesario. Cualquier elemento de UI que se agregue en el root layout se compartirá en toda la app. El root layout se puede usar para modificar las etiquetas `<html>` y `<body>`, además de agregar metadata.

## Navegación

En Next.js se puede usar el componente `<Link />` para vincuar las paginas en una app. Este componente permite realizar el *client-side navigation* con JavaScript.

```tsx
import Link from 'next/link';

export default function NavLinks() {
  return (
    <>
      {links.map((link) => {
        const LinkIcon = link.icon;
        return (
          <Link
            key={link.name}
            href={link.href}
            className="estilos"
          >
            <LinkIcon className="w-6" />
            <p className="hidden md:block">{link.name}</p>
          </Link>
        );
      })}
    </>
  );
}
```

El componente `<Link />` es muy similar a la etiqueta `<a>`.

La diferencia entre usar `<Link />` y `<a>` es que no sé recarga la página completa, mejorando la UX. Las partes de la app se renderizan en el servidor, pero no hay una recarga completa de la página, ¿Por qué?

Next.js automáticamente hace un *code-split* de la app por segmentos de ruta. Esto es diferente a una SPA de React, donde el navegador carga todo el código de la app en la carga inicial.

Hacer *code-spliting* por rutas significa que las páginas quedan aisladas. Si cierta página lanza un error, el resto de la app igual continuará funcionando.

Cada vez que el componente `<Link />` aparece en el viewport del navegador, Next.js automaticamente hace un prefetch del codigo vinculado para la ruta en segundo plano. Cuando el user haga click en el link, el codigo de la página de destino ya estará cargado en segundo plano, esto hace que la transición sea casi instantanea.

Next.js provee un hook llamado `usePathname()`. Se usará este hook en la app para indicar visualmente en que ruta se encuentra el user.

`usePathname()` es un hook, entonces se necesita convertir el fichero donde se usa en un Client Component usando la directiva `"use client"`, ya que por defecto, los compoentes de Next.js son Server Component

```tsx
"use client";

import Link from 'next/link';
import { usePathname } from 'next/navigation';
// ...
export default function NavLinks() {
  const pathname = usePathname();

  return (
    <>
      {links.map((link) => {
        const LinkIcon = link.icon;
        return (
          <Link
            key={link.name}
            href={link.href}
            className={`flex h-[48px] grow items-center justify-center gap-2 rounded-md bg-gray-50 p-3 text-sm font-medium hover:bg-sky-100 hover:text-blue-600 md:flex-none md:justify-start md:p-2 md:px-3 
	            ${pathname === link.href ? 'bg-sky-100 text-blue-600' : ''}
            `}
	          >
            <LinkIcon className="w-6" />
            <p className="hidden md:block">{link.name}</p>
          </Link>
        );
      })}
    </>
  );
}
```

## Fetching data:

Se puede usar una capa de APIs. Hay unos cuantos casos de uso en los que se podría usar una API, por ejemplo, si se usa un servicio de tercero que provee una API o si se está obteniendo datos del cliente, es necesaria una capa de API que corra en el server para evitar exponer la base de datos al cliente.

En Next.js se puede crear endoints de API usando *Route Handlers*.

También se puede usar **queries de base de datos**. Para base de datos relacionales se puede usar SQL o un ORM. 

Cuando se crea los endpoints de la API, se necesita escribir lógica que interactue con la base de datos. Además, sí se usa **React Server Components** (el fetching se hace en el server), se puede saltar la capa de API y hacer las consultas sin riesgos de exponer la base de datos al cliente.

Por default, Next.js usa React Server Components.  hacer fetching de datos con Server Components es un enfoque relativamente nuevo y tiene unos beneficios.

Los **Server Components** soportan promesas, proveyendo una solucion más simple para las tareas asincronas como el fetching de datos. Se puede usar la sintaxis `async/await` sin recurrir al `useEffect`, `useState` u otras librerias de fetching.

Los **Server Components** se ejecutan en el server, así que se puede hacer fetching de datos y lógica pesada en el server y solo se enviará el resultado al cliente.

Para escribir SQL, Vercel provee la funcion `sql` de `@vercel/postgres`. Esta funcion permite escribir consultas.

### Fetching en un Server Component:

```tsx
// otros imports
import { fetchRevenue } from '../lib/data';
import { fetchLatestInvoices } from '../lib/data';
import { fetchCardData } from '../lib/data';

export default async function Dashboard() {
  const revenue = await fetchRevenue();
  const latestInvoices = await fetchLatestInvoices();
  const { 
	  numberOfCustomers, 
	  numberOfInvoices, 
	  totalPaidInvoices, 
	  totalPendingInvoices 
	} = await fetchCardData();

    return (
    <main>
      <h1 className={`${lusitana.className} mb-4 text-xl md:text-2xl`}>
        Dashboard
      </h1>
      <div className="grid gap-6 sm:grid-cols-2 lg:grid-cols-4">
        <Card
          title="Collected"
          value={totalPaidInvoices}
          type="collected"
        />
        <Card
          title="Pending"
          value={totalPendingInvoices}
          type="pending"
        />
        <Card
          title="Total Invoices"
          value={numberOfInvoices}
          type="invoices"
        />
        <Card
          title="Total Customers"
          value={numberOfCustomers}
          type="customers"
        />
      </div>
      <div className="mt-6 grid grid-cols-1 gap-6 md:grid-cols-4 lg:grid-cols-8">
        <RevenueChart revenue={revenue} />
        <LatestInvoices latestInvoices={latestInvoices} />
      </div>
    </main>
  );
}
```

El componente Dashboard es una función asincrona, lo cuál hace que el fetching de datos sea mucho más fácil y eficiente.

Acá pasan dos cosas:

1. Se crea una **casacada de peticiones** que se bloquean una a otras de forma inintencionada.
2. Por defecto, Next.js **pre-renderiza** las rutas para mejorar el rendimiento, esto se llama **Static Rendering**. Así que, si los datos cambián, no se verán reflejados.

La **cascada** se refiere a la secuencia de peticiones que depende de la completitud de la peticion previa. Por ejemplo, se necesita esperar que `fetchRevenue()` termine de ejecutarse para que `fetchLatestInvoices()` empiece a ejecutarse:

```tsx
const revenue = await fetchRevenue();
// espera que fetchRevenue() termine
const latestInvoices = await fetchLatestInvoices();
const {
  numberOfInvoices,
  numberOfCustomers,
  totalPaidInvoices,
  totalPendingInvoices,
} = await fetchCardData(); // espera que fetchLatestInvoices() termine
```

Este patron no es necesariamente malo, hay casos en donde se querrá usar **cascadas** porque se espera que se cumpla una condición antes de hacer la siguiente petición.

En cualquier caso, este comportamiento también puede ser inintencional y impactar el rendimiento.

La forma más común de evitar las **cascadas** es iniciar toas las peticiones al mismo tiempo, en paralelo. En JavaScript se puede usar `Promise.all()` o `Promise.alSettled()`. Esto puede mejorar el rendimiento. Sin embargo, hay una desventaja, qué pasa si una petición es más lenta que las otras?

### Renderizado Estático:

Con el renderizado estático, el fetching de datos pasa en el server en build-time o cuando se revalidan los datos.

Cuando un usuario visita la app, el resultado cacheado es servido, esto tiene sus ventajas: 

- Las páginas son más rápidas ya que, el contenido del prerederizado puede ser cacheado.
- Reduce la carga del server porque el contenido es cacheado, entonces, el server no tiene que generar dinamicamente contenido para cada petición del usuario.
- SEO, ya que el contenido prerenderizado es más fácil de indexar para los rastreadores de los motores de búsqueda, ya que el contenido ya está disponible cuando se carga la página.

El renderizado estatico es útil para UIs sin datos o para datos que se comparten entre usuarios como un post estático de blog o una página de productos. No es tan buena para dasboards que tiene datos personalizados que se actualizan con regularidad.

### Renderizado dinámico:

Con este renderizado, el contenido es renderizado en el server para cada petición del usuario.

Beneficios:

- El renderizado dinámico permite mostrar datos en tiempo real o con actualizaciones frecuentes.
- Es más fácil srvir contenido personalizado, como en un dashboard o perfiles de usuario y actualizar los datos de acuerdo a la interación de los usuarios.
- Permite acceso a información que puede ser accesible solo en tiempo de peticion, como las cookies o los seach params de la URL.

## Streaming

Es una tecnica de transferencia de datos que permite dividir una ruta en fragmentos más pequeños llamados *chunks* y progresivamente servirlos desde el servidor al cliente cuando estos estén listos.

Evita que request lentas bloqueen toda la página.

El streaming funciona bien con los componentes de React, cada componente puede ser considerado como un *chunk.*

Se puede implementar de dos formas: `loading.tsx` a nivel de toda la página y `<Suspense>` para un componente en especifico.

`loading.tsx` es un archivo especial de Next.js, permite crear una interfaz alternativa para mostrar mientras carga el contenido de la página.

```tsx
import DashboardSkeleton from '@/app/ui/skeletons';
 
export default function Loading() {
  return <DashboardSkeleton />;
}
```

Ya que `loading.tsx` tiene un nivel superior, también se aplica a las páginas de invoices y customers por igual. Esto se puede evitar con los Route Groups.

Dentro de la carpeta del dashboard se crea otra carpeta llamada `/(overview)`. Ahora `loading.tsx` solo se aplica al overview del dashboard.

Las Rutas Agrupadas permiten organizar archivos en grupos lógicos sin afectar la URL. Acá se usa rutas agrupadas para asegurar que `loading.tsx` solo se aplique al overview del dashboard.

También se puede aplicar el streaming a componentes, siendo más granlar usando el Suspense de React.

Suspense permite suspender la renderización de un componente hasta que se cumpla una condición, por ejemplo cunado los datos terminan de cargarse. Se puede envolver el componente dinámico con un Suspense, se pasa un componente para el fallback para mostrar mientras el componente dinámico carga.

```tsx
// otros imports
import { Suspense } from 'react';
import { LatestInvoicesSkeleton, RevenueChartSkeleton } from '@/app/ui/skeletons';

export default async function Dashboard() {
	// ...

  return (
    // ...
      <div className="mt-6 grid grid-cols-1 gap-6 md:grid-cols-4 lg:grid-cols-8">
        <Suspense fallback={<RevenueChartSkeleton />}>
          <RevenueChart />
        </Suspense>
        <Suspense fallback={<LatestInvoicesSkeleton />}>
          <LatestInvoices />
        </Suspense>
      </div>
    </main>
  );
}
```

`revenue-cart.tsx`:

```tsx
// otros imports
import { fetchRevenue } from '@/app/lib/data';
 
// ...
// Make component async, remove the props
export default async function RevenueChart() { 
  const revenue = await fetchRevenue(); // Fetch data inside the component
 
  // ...
 
  return (
    // ...
  );
}
 
```

`latest-invoices.tsx`:

```tsx
// otros imports
import { fetchLatestInvoices } from '@/app/lib/data';
 
export default async function LatestInvoices() { // Remove props
  const latestInvoices = await fetchLatestInvoices();
 
  return (
    // ...
  );
}
```

## Partial prerendering:

Para la mayoria de apps se tiene que elegir entre renderizado dinámico y estático para toda la app o para una ruta especifica. En Next.js, si se quiere llamar a una función dinámica en una ruta, toda la ruta se convierte en dinámica.

La mayria de las rutas no son enteramente dinámicas o estáticas. Considerando un ecommerce, se querrá renderizar estáticamente la mayoría de la información del producto, pero renderizar dinámicamente el carrito y los productos recomendados.

El prerenderizaso parcial es una técnica que permite generar y servir ciertas partes de una página de manera estática mientras otras partes se renderizan dinámicamente en server-side o client-side.

El partial prerendering usa el Suspense de React para diferirlas partes del renderizado de la app hasta que cierta condición se cumpla.

El fallback de Suspense está incrustado en el HTML inicial con el contenido estático. En build time el contenido estático es prerenderizado para crear un shell estático. El renderizado de contenido dinámico se pospone hasta que el usuario haga una petición a la ruta.

Envolver un componente en un Suspense no hace el componente dinámico por si mismo, Suspense se usa como limite entre código estático y dinámico.

Así se habilita el Prerenderizado Parcial:

```tsx
/** @type {import('next').NextConfig} */

const nextConfig = {
  experimental: {
    ppr: 'incremental', // con estas lineas de código.
  },
};

export default nextConfig;

```

El valor `'incremental'` permite adoptar el Renderizado Parcial para rutas especificas.

Luego se agrega el siguiente linea de configuración en el layout del dashboard:

```tsx
export const experimental_ppr = true;
```

Estos cambios no se nota en desarrollo pero si en producción. Next.js va a prerenderizar las partes estáticas de la ruta y va a diferir las partes dinámicas hasta que el usuario haga un request de ellas.

Lo mejor del PPR es que no se necesita cambiar el código para usarlo, siempre y cuando se use Suspense para envolver las partes dinámicas de las rutas, Next.js sabra que partes de las rutas son estáticas y dinámicas.

## Busqueda y páginación

Para manejar busquedas es recomendable usar los URL search params, esto permite compartir URLs de una busqueda, facilita el manejo y la carga inicial ya que las URLs se pueden consumir directamente en el servidor además tener los filtros y queries de busquea en la URL hace más facil seguir el comportamiento del usuario sin necesidad de lógica adicional en el cliente.

Hooks para implementar la funcionalidad de busqueda:

- `useSearchParams`: permite acceder a parametros de la URL acutal. Por ejemplo, los parametros de la siguiente URL `/dashboard/invoices?page=1&query=pending` son estos: `{page: '1', query: 'pending'}`.
- `useParams`: permite leer el pathname de la URL acutal. Por ejemplo la ruta  `dashboard/invoices`, retornará `'/dashboard/invoices'`.
- `useRouter`: permite la navegación entre rutas dentro de los componentes del cliente.

Para usar estos hooks además de event listeners, se debe usar la directiva `"use client` para indicar que el componente es un Client Component.

Una buena practica seria imlementar el debouncing para limitar la frecuencia en la que una función es invocada, en el caso de la busqueda, la función se llama cada vez que se presiona una tecla.

## Server Actions

Los Server Actions de React permite ejecutar código asincrono en el servidor. Elimina la necesidad de crear API endpoints para mutar datos.

Ofrecen una solución de seguridad efectiva, protegiendo en contra de diferente tipos de ataques, asegurando datos y acceso autorizado.

En React se puede usar el atributo `action` en el elemento `<form>` para invocar acciones. La acción recibirá automáticamente el objeto `FormData`, conteniendo los datos capturados.

```tsx
// Server Component
export default function Page() {
  // Action
  async function create(formData: FormData) {
    'use server';
    // Logica para mutar datos
  }
 
  // Invocar la accion usando el atributo "action"
  return <form action={create}>...</form>;
}
```

Una ventaja de usar Server Actions en los Server Components es que los forms funcionan incluso sin el JavaScript esta desactivado en el cliente.

Las Server Actions están profundamente integradas con el caching de Next.js. Cuando un formulario es enviado a través de un Server Action, no solo se puede usar la accion para mutar datos, sino también para revalidar el cache asociado usando APIs como `revalidatePath` y `revalidateTag`.

## Manejo de Errores

Next.js tiene el archivo especial llamado `error.tsx`, este archivo puede usarse como limite de la UI para un segmeto de ruta. 

Sirve como un comodin para errores inesperados y permite tener una UI fallback para los usuarios.

`error.tsx` necesita ser un Client Component, acepta dos props:

- `error`: instancia del objeto `Error` de JavaScript.
- `reset`: funcion que resetea el limite de error. Cuando se ejecuta la funcion intentará re-renderizar el segmeto de ruta.

Otra forma de manejar erroes es usando la función `notFound`. Mientras que `error.tsx` es util para atrapar TODOS los errores, `notFound` es usado cuando se trata de hacer fetch a algo que no existe.

```tsx
import { notFound } from 'next/navigation';
 
export default async function Page({ params }: { params: { id: string } }) {
  const id = params.id;
  const [invoice, customers] = await Promise.all([
    fetchInvoiceById(id),
    fetchCustomers(),
  ]);
 
  if (!invoice) {
    notFound();
  }
  // ...
}
```

`notFound` toma precedencia sobre `error.tsx`, para recurrir a él cuando se necesita manejar errores más especificos.

## Mejorando accesibilidad

Next.js incluye el plugin `eslint-plugin-jsx-ally` que permite detectar errores de accesibilidad. Este plugin advierte por ejemplo cuando una imagen no tiene el atributo `alt`.

### Client-Side Validation

Lo más sencillo es confar en la validación que provee el navegador agregado el atributo `required` a las etiquetas `input`y `select` en el form.

```tsx
<input
  id="amount"
  name="amount"
  type="number"
  placeholder="Enter USD amount"
  className="peer block w-full rounded-md border border-gray-200 py-2 pl-10 text-sm outline-2 placeholder:text-gray-500"
  required
/>
```

### Server-Side validation

Validando formularios en el servidor asegura que los datos tengan el formato esperado antes que se envien a la base de datos, reduce el riesgo de usuarios maliciosos y tener una fuente de la verdad para lo que se considera datos validos. 

Para esto se usa el hook de react `useActionState`:

```tsx
'use client';
// ...
import { useActionState } from 'react';
```

Tiene dos argumentos: `(action, initialState)`. Retorna dos valores `[state, formAction]` - el estado del formulario y la funcion que será llamada cuando se envie el form.

## Agregar Autenticación

Una web segura usa multiples formas de chequear la identidad de un usuario.

La autenticación chequea quien es el usuario y la autorización determina a que partes de la app el usuario puede acceder.

En el tutorial se usa `NextAuth.js` para agregar autenticación a la app. NextAuth abstrae cierta complejidad haciendo más facil, rapido y disminuyendo la posibilidad de errores.

Despues de instalar `NextAuth.js` es importante generar na key para la app. Esta key es usada para encriptar la cookies, asegurando la sesión del usuario:

```bash
openssl rand -base64 32 
```

## Agregar metadata

Next.js tiene una API de Metadata que se puede usar para definir los metadatos de la aplicación. Next.js automáticamente generará los elementos relevantes para el `<head>` en la página.

Se puede incluir el objeto `metadata` en cualquier archivo `layout` o `page` para agregar información como el titulo o descripción.

```tsx
// /app/layout.tsx
import { Metadata } from 'next';
 
export const metadata: Metadata = {
  title: 'Acme Dashboard',
  description: 'The official Next.js Course Dashboard, built with App Router.',
  metadataBase: new URL('https://next-learn-dashboard.vercel.sh'),
}; 
```

Next.js agregará automátcamente el titulo y la descripción a la aplicación.

Se puede agregar metadata para páginas especificas, ya que se sobrescribe los metadatos del padre.

```tsx
// /app/dashboard/invoices/page.tsx
import { Metadata } from 'next';
 
export const metadata: Metadata = {
  title: 'Invoices | Acme Dashboard',
};
```

Lo que pasa es que haciendo esto se repite el titulo en cada pagina. Para solucionar esto se usa el `title.templane`:

```tsx
// /app/layout.tsx
import { Metadata } from 'next';
 
export const metadata: Metadata = {
  title: {
    template: '%s | Acme Dashboard',
    default: 'Acme Dashboard',
  },
  description: 'The official Next.js Learn Dashboard built with App Router.',
  metadataBase: new URL('https://next-learn-dashboard.vercel.sh'),
};
```

`%s` es el template que será reemplazado con el titulo especifico de cada pagina.

```tsx
// /app/dashboard/invoices/page.tsx
export const metadata: Metadata = {
  title: 'Invoices',
};
```