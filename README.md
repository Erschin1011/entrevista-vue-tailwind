# Plantilla de entrevista: Vue + JavaScript + Tailwind CSS

Frontend listo para clonar con **Vue 3**, **JavaScript**, **Vite** y **Tailwind CSS 4**. Incluye una pantalla pequeña e interactiva para comprobar que Vue, Vite y Tailwind funcionan antes de empezar el ejercicio.

## Índice

1. [Qué incluye](#qué-incluye)
2. [Instalar Node.js y herramientas](#instalar-nodejs-y-herramientas)
3. [Clonar e instalar](#clonar-e-instalar)
4. [Iniciar, compilar y detener](#iniciar-compilar-y-detener)
5. [Uso de Tailwind y Vue](#uso-de-tailwind-y-vue)
6. [Conectar a una API](#conectar-a-una-api)
7. [Problemas frecuentes](#problemas-frecuentes)

## Qué incluye

- Vue 3 y JavaScript (no TypeScript).
- Vite como servidor de desarrollo y bundler.
- Tailwind CSS 4 con su plugin oficial de Vite.
- Ejemplo de `ref`, `computed`, `v-model`, `v-for`, eventos, agregar y quitar tareas.
- Build de producción verificable.
- No incluye backend, base de datos, Laravel ni Express.

## Instalar Node.js y herramientas

Instala **Node.js LTS** desde [nodejs.org](https://nodejs.org/); npm viene incluido. En el instalador de Windows deja habilitado agregar Node al PATH y cierra/abre PowerShell al terminar.

```powershell
node --version
npm --version
where.exe node
```

Se recomienda Node 20 o superior. Instala Git for Windows desde [git-scm.com/download/win](https://git-scm.com/download/win) para clonar. VS Code es opcional.

**No tienes que instalar Vue ni Tailwind globalmente.** El repo declara sus versiones en `package.json` y `package-lock.json`; npm las instala localmente al proyecto.

## Clonar e instalar

```powershell
git clone https://github.com/Erschin1011/entrevista-vue-tailwind.git
cd entrevista-vue-tailwind
powershell -ExecutionPolicy Bypass -File .\scripts\setup.ps1
```

El script verifica Node/npm, instala las dependencias reproducibles (`npm ci`) y compila el proyecto.

Equivalente manual:

```powershell
npm ci
npm run build
```

Usa `npm ci` tras clonar o cambiar de máquina. Si agregas o actualizas paquetes, usa `npm install <paquete>` y conserva el `package-lock.json` actualizado.

## Iniciar, compilar y detener

Desde la raíz del repo:

```powershell
npm run dev
```

Abre la dirección local que Vite imprime (normalmente `http://localhost:5173`). Deja esa terminal encendida mientras trabajas; para detenerlo presiona `Ctrl+C`.

Comandos diarios:

```powershell
npm run dev       # desarrollo y hot reload
npm run build     # build de producción en dist/
npm run preview   # previsualiza dist localmente
npm test          # aún no hay suite de pruebas para la UI
npm ls --depth=0  # listar dependencias directas
npm audit         # comprobar avisos de seguridad de dependencias
```

No subas `node_modules/` ni `dist/`; `.gitignore` ya los excluye. En producción publica el contenido generado en `dist/` usando el hosting que indique el ejercicio.

## Uso de Tailwind y Vue

Archivos principales:

- `src/App.vue`: pantalla Vue y lógica de ejemplo; reemplázala con la interfaz que pida la prueba.
- `src/main.js`: crea la app y monta `App.vue` en `#app`.
- `src/style.css`: importa Tailwind con `@import "tailwindcss"` y define defaults globales.
- `vite.config.js`: conecta el plugin oficial `@tailwindcss/vite` y el plugin de Vue.
- `index.html`: documento inicial cargado por Vite.

Tailwind 4 se configura por CSS y el plugin de Vite; para comenzar **no hace falta `tailwind.config.js`** ni ejecutar `npx tailwindcss init`.

## Conectar a una API

Si el reto incluye un backend, crea un módulo como `src/services/posts.js` para agrupar `fetch`/Axios y llama esas funciones desde componentes. Si la URL es configurable, crea `.env.local` (ignorado por Git) con:

```dotenv
VITE_API_URL=http://127.0.0.1:8000/api
```

En Vite solo las variables que empiezan por `VITE_` se exponen al código cliente; **no guardes secretos** en ellas. Laravel y Vue son servidores separados en desarrollo: una API local debe permitir el origen de Vite mediante CORS si el navegador lo requiere.

Para añadir Axios:

```powershell
npm install axios
```

La plantilla no necesita Axios mientras no se conecte a un backend.

## Problemas frecuentes

| Problema | Solución |
|---|---|
| `node` o `npm` no se reconoce | Reinstala Node LTS con PATH habilitado y abre una terminal nueva. |
| `Missing script: dev` | Confirma estar en la raíz del proyecto y que exista `package.json`. |
| Puerto 5173 ocupado | Vite ofrecerá otro puerto en terminal; abre la URL que indique. |
| Tailwind no aplica clases | Comprueba `@import "tailwindcss"` en `src/style.css`, plugin en `vite.config.js` y reinicia Vite. |
| Build no encuentra paquetes | Corre `npm ci` desde la raíz del repo. |
| Error CORS al llamar Laravel/Express | Revisa que backend y frontend estén activos y habilita el origen local de Vite en el backend. |

Este starter usa JavaScript plano. Si después quieres TypeScript, puedes añadirlo como decisión propia, pero no es requisito para ejecutar la plantilla.
