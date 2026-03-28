---
title: "Componentes integrados en React JS"
date: 2025-10-12T07:30:17+02:00
lastmod: 2025-10-12T07:30:17+02:00
author: Fco. Javier Cousiño
categories:
  - ReactJS
tags:
  - ReactJS
  - JavaScript
  - Frontend
draft: false
---

## `<Fragment>`

#### __Referencia__

Te permite agrupar varios nodos JSX juntos. La etiqueta JSX vacía `<></>` es la abreviatura de `<Fragment></Fragment>`. Los Fragmentos son útiles porque la agrupación de elementos con un Fragmento no tiene efecto en el diseño o los estilos, al contrario de cómo sería si envolvieras los elementos dentro de cualquier otro contenedor tal como un elemento del DOM.

#### __Props__

+ key: el atributo key puede ser usado de manera opcional en el componente Fragment.

#### __Advertencias__

+ Si quisieras pasarle una key a un Fragmento, no podrias usar la sintaxis `<>...</>`. Tendrias que importar explícitamente Fragment desde 'react' y renderizar `<Fragment key={yourKey}>...</Fragment>`.
+ React no reinicia el estado cuando renderizas desde un `<><Child /></>` a un `[<Child />]` y viceversa, o cuando renderizas desde un `<><Child /></>` a un `<Child />` y viceversa. Ten en cuenta de que esto sólo funciona a un nivel de profundidad: por ejemplo, ir desde un `<><><Child /></></>` a un `<Child />` reinicia el estado.

#### __Ejemplo__

        function CloseDialog() {
            const buttons = (
                <>
                <OKButton />
                <CancelButton />
                </>
            );
            return (
                <AlertDialog buttons={buttons}>
                Are you sure you want to leave this page?
                </AlertDialog>
            );
        }   

## `<Profiler>`

#### __Referencia__

Mide el rendimiento de la renerización de un árbol de React de manera 
programática. Envuelve un árbol de componentes en un `<Profiler` para medir su rendimiento de renderizado.

#### __Props__

+ id: string que identifica que parte de la interfaz de usuario estás midiendo.
+ onRender: un callback onRender que React llama cada vez que los componenentes dentro del árbol perfilado se actualizan. Recibe información sobre lo que se renderizó y cuánto tiempo llevó.
    + id: id del profiler que se entregó. Esto permite identificar que parte del árbol se entregó si estás usando varios perfiles.
    + phase: ("mount", "update", "nested-update") indica si el árbol acaba de ser montado por primera vez o se ha vuelto a renderizar debo a un cambio en las props, el estado o los hooks. 
    + actualDuration: milisegundos que tardó en renderizar.Este valor debería disminuir después del montaje inicial, ya que los descendientes sólo se renderizarán si cambian sus propiedades.
    + baseDuration: milisegundos que estima cuánto tiempo tarda en volver a renderizar. Se suman las duraciones del renderizado de cada componente del árbol. Compara `actualDuration` con este valor para ver si la memorización está funcionando.
    + startTime: marca de tiempo desde que React empezó a renderizar.
    + endTime: tiempo final de la renderización.


            function onRender(id, phase, actualDuration, baseDuration, startTime, commitTime) {
                // Agregar o registrar tiempos de procesamiento...
            }

#### __Advertencias__

+ Agrega cierta sobrecarga adicional, por lo que en el entorno de producción está deshabilitado por defecto.

#### __Ejemplo__

        <App>
            <Profiler id="Sidebar" onRender={onRender}>
                <Sidebar />
            </Profiler>
            <Profiler id="Content" onRender={onRender}>
                <Content>
                <Profiler id="Editor" onRender={onRender}>
                    <Editor />
                </Profiler>
                <Preview />
                </Content>
            </Profiler>
        </App>

## `<Suspense>`

#### __Referencia__

Muestra un sustituto mientras los componentes hijos se están cargando.

#### __Props__

+ children: interfaz que realmente se pretende renderizar. Si `children` se suspende mientras se renderiza, la barrera de Suspense pasará a renderizar `fallback`.
+ fallback: interfaz alternativa a renderizar en lugar de la interfaz real. Se acepta cualquier nodo de React, auqnue suele ser una vista ligera de relleno (spinner de carga). Suspense cambiará automáticamentea `fallback` cuando `children` se suspenda y volverá a `children` cuando los datos estén listos. Si `fallback` se suspende mientras se renderiza, activará la barrera de Suspense padre más cercana.

#### __Advertencias__

+ No preserva ningún estado para los renderizados que  suspendieron antes de que pudiera montarse por primera vez. Cuando el componente se haya cargado, React volverá a intentar renderizar el árbol suspendido desde cero.
+ Si la suspensión estaba mostrando contenido para el árbol, pero luego se volvió a suspender, el fallback se mostrará de nuevo a menos que la actualización que lo causó fuese causada por `startTransition` o `useDeferredValue`.
+ Si React necesita ocultar el contenido ya visible porque se suspendió de nuevo, limpiará los Efectos de layout en el árbol de contenido. Cuando el contenido esté listo para mostrarse de nuevo, React disparará los Efectos de layout de nuevo. Esto le permite asegurarse de que los Efectos que miden el diseño del DOM no intentan hacerlo mientras el contenido está oculto.
+ React incluye optimizaciones internas como Renderizado en el servidor con Streaming e Hidratación selectiva que se integran con Suspense. Puedes leer una visión general de la arquitectura y ver esta charla técnica para conocer más.

#### __Ejemplo__

        import { Suspense } from 'react';
        import Albums from './Albums.js';
        import Biography from './Biography.js';
        import Panel from './Panel.js';

        export default function ArtistPage({ artist }) {
        return (
            <>
                <h1>{artist.name}</h1>
                <Suspense fallback={<Loading />}>
                    <Biography artistId={artist.id} />
                    <Panel>
                        <Albums artistId={artist.id} />
                    </Panel>
                </Suspense>
            </>
            );
        }

        function Loading() {
            return <h2>🌀 Loading...</h2>;
        }

## `<ScriptMode>`

#### __Referencia__

Permite controles adicionales solo para el desarrollo que te ayudan a encontrar errores anticipadamente. Usa `StrictMode` para habilitar comportamientos de compilación y advertencias adicionales (Modo Estricto) dentro del árbol de componentes

El Modo Estricto habilita los siguientes comportamientos solo en desarrollo:

+ Los componentes se volverán a renderizar una vez más para encontrar errores causados por renderizaciones impuras.
+ Tus componentes volverán a ejecutar los Efectos una vez más para encontrar errores causadas por la ausencia de la fase de limpieza de estos.
+ Se comprobará el uso en tus componentes de APIs obsoletas.

#### __Props__

+ `StringMode`, no acepta props.

#### __Advertencias__

+ No hay forma de excluirse del Modo Estricto dentro de un árbol envuelto en `<StrictMode>`. Esto te asegura de que se comprueban todos los componentes dentro de `<StrictMode>`. Si dos equipos que trabajan en un producto no están de acuerdo sobre si le resultan valiosas estas comprobaciones, necesitarían o bien llegar a un consenso o bien mover `<StrictMode>` abajo en el árbol.

#### __Ejemplo__

        import { StrictMode } from 'react';
        import { createRoot } from 'react-dom/client';

        const root = createRoot(document.getElementById('root'));
        root.render(
        <StrictMode>
            <App />
        </StrictMode>
        );