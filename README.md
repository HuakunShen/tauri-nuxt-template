# Tauri + Nuxt 3 Template

This is a minimal template to combine Tauri and Nuxt 3.

This template is constructed completely with official template from Tauri and Nuxt 3.

Tauri API has been verified to work with Nuxt, just make sure `ssr` is `false` in [nuxt.config.ts](./nuxt.config.ts). 

The code used to verify tauri API has been removed to keep the template as clean as possible. `@tauri-apps/api` has been installed though.

## Usage

You could click `Use this template` on GitHub, or simply make a copy of this repo. See the [Auto Script](#auto-script-for-generating-a-template) section for a auto template generation script.

## Auto Script for Generating a Template

This repo will not be always up to date with the latest nuxt and Tauri versions, so if you really want to use the latest version of Tauri and Nuxt, use the script below. The script is also avaialble at [./gen-tauri-nuxt.sh](./gen-tauri-nuxt.sh).

Run it like this `./gen-tauri-nuxt.sh $YOUR_APP_NAME`.

Or this, so you don't need to download or copy anything.

```bash
wget https://raw.githubusercontent.com/HuakunShen/tauri-nuxt-template/main/gen-tauri-nuxt.sh
sh gen-tauri-nuxt.sh
```

It's pretty much completely automatic, but you still need to interact with the shell script prompt. Make sure `npm run generate` is used instead of the default `npm run build`, run it and you will see.

```bash
# gen-tauri-nuxt.sh
APP_NAME=$1
if [ -z "$APP_NAME" ]; then
    echo "Please provide the app name as the first argument"
    read APP_NAME
fi

npx nuxi init $APP_NAME
cd $APP_NAME
npm i

echo "// https://nuxt.com/docs/api/configuration/nuxt-config
export default defineNuxtConfig({
    devtools: { enabled: true },
    ssr: false // SSR must be turned off
})" > nuxt.config.ts
npm install --save-dev @tauri-apps/cli
# use sed to add "tauri": "tauri" to package.json -> scripts
sed -i '' 's/"postinstall": "nuxt prepare"/"postinstall": "nuxt prepare",\n    "tauri": "tauri"/g' package.json
echo "\033[0;31m\nFor the following questions,\nkeep defaults for all questions except for the 'frontend build command'. \nUse 'npm run generate' \n\033[0m"
npm run tauri init
# need user interaction here
# Keep defaults for all questions except for the frontend build command
# use `npm run generate`
npm install @tauri-apps/api
```