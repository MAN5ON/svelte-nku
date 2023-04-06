# Тестовое задние для НКУ 

## Описание задачи:

**Необходимо разработать простую программу используя NodeJS + TypeScript + Svelte Kit, которая будет читать значение мощности c MQTT сервера и отправлять новое значение при движении ползунка. Если открыть несколько вкладок в браузере при изменении значения в одном месте оно автоматически будет меняться во всех вкладках. Этот блок необходимо реализовать как отдельный компонент Svelte. MQTT сервер (брокер) используйте этот: Mosquitto Test**

## Реализация:

- **Для подключения к MQTT брокеру я использовал библиотеку [mqtt.js](https://github.com/mqttjs/MQTT.js)**

На этом пункте сразу же появилось много проблем, т.к. библиотека использует в работе **`Buffer`**, который есть в **Node JS**, но отсутствует в Браузере. Из нескольких десятков вариантов (как рабочих, так и нерабочих) я выбрал вариант с установкой библиотеки **[NodeGlobalsPolyfillPlugin](https://www.npmjs.com/package/@esbuild-plugins/node-globals-polyfill)** и добавлением **`Buffer`** в **Vite.config.ts**

- **Одно значение на всех вкладках**

Для реализации этой функции я добавил несколько проверок в код, чтобы отловить неожиданное поведение *(например NaN при первом рендере)*  или не вызывать функцию, если значение мощности на Брокере и клиенте одинаково, а так же добавил значение мощности в **localStorage**, и обновляю его в случае изменения

- **Style**

Для стилизации приложения я использовал CSS фреймворк [Tailwind](https://tailwindcss.com/)

В случае возникновения вопросов по реализации - с радостью отвечу в ТГ.


---

# create-svelte

Everything you need to build a Svelte library, powered by [`create-svelte`](https://github.com/sveltejs/kit/tree/master/packages/create-svelte).

Read more about creating a library [in the docs](https://kit.svelte.dev/docs/packaging).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```bash
# create a new project in the current directory
npm create svelte@latest

# create a new project in my-app
npm create svelte@latest my-app
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

Everything inside `src/lib` is part of your library, everything inside `src/routes` can be used as a showcase or preview app.

## Building

To build your library:

```bash
npm run package
```

To create a production version of your showcase app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.

## Publishing

Go into the `package.json` and give your package the desired name through the `"name"` option. Also consider adding a `"license"` field and point it to a `LICENSE` file which you can create from a template (one popular option is the [MIT license](https://opensource.org/license/mit/)).

To publish your library to [npm](https://www.npmjs.com):

```bash
npm publish
```
