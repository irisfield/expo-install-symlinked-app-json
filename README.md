# `npx expo install` replaces a symlinked `app.json` with a regular file

`app/app.json` is a symlink to `shared/app.json`.

## Steps

1. Run `cd app && npm install`.
2. Run `ls -l app.json`. It shows `app.json -> ../shared/app.json`.
3. Run `npx expo install expo-build-properties`.
4. Run `ls -l app.json` and `cat ../shared/app.json`.

## Actual

`npx expo install` prints `Added config plugin: expo-build-properties`.

`app/app.json` is now a regular file that contains the `plugins` entry. `shared/app.json` has no `plugins` entry and is unchanged.

## Expected

`app/app.json` is still a symlink to `shared/app.json`, and `shared/app.json` contains the `plugins` entry.

## Also

The file mode is not kept either. With a regular `app.json` set to mode `600` (or `755`), the same command leaves it at `644`.
