# vue-typescript-cheatsheet

Cheatsheets for experienced Vue developers getting started with TypeScript

- https://devchat.tv/views-on-vue/vov-076-typescript-tell-all-with-jack-koppa/


## Recommended ts.config setup
note: `strict:true` stricter inference for data properties on `this`. If you do not use it, `this` will always be treated as `any`
```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "esnext",
    "strict": true,
    "moduleResolution": "node"
  }
}
```

## Usage in .vue files
add `lang="ts"` to the script tag to declare TS as the lang used.
```html
<script lang="ts">
  ...
</script>
```
