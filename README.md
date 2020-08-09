# vue-typescript-cheatsheet

Cheatsheets for experienced Vue developers getting started with TypeScript

- https://devchat.tv/views-on-vue/vov-076-typescript-tell-all-with-jack-koppa/


## Recommended ts.config setup
```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "esnext",
    // this enables stricter inference for data properties on `this`
    "strict": true,
    "moduleResolution": "node"
  }
}
```
