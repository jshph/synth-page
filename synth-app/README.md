# synth-app

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

## Other setup for Tone.JS

Vue doesn't allow for Tone.JS to load an audio file from `file://` because it interprets paths as Webpack-relative. In order to serve audio files to be used by the app, navigate to `src/assets/audio` and run `http-server -p 3000 --cors`. Install with `npm install http-serve` if you haven't already. `SynthTone.vue` references a file served by this local server.