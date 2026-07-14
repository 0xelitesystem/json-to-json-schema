# JSON to JSON Schema

Paste a JSON sample and generate a JSON Schema (draft 2020-12) that describes its shape. The tool infers types, marks present keys as required, builds item schemas for arrays, recurses into nested objects, detects common string formats, and turns small repeated string sets into enums. Everything runs in your browser with no external dependencies and works offline.

## Live demo

https://0xelitesystem.github.io/json-to-json-schema/

## Features

- Draft 2020-12 output with the `$schema` keyword set for you.
- Type inference: `string`, `integer`, `number`, `boolean`, `null`, `object`, `array`.
- Required properties: choose required = present keys, or required = none.
- Arrays: infers an item schema from the elements and merges mixed elements into one shape (union of primitive types, merged object fields).
- Nested objects: recurses to any depth.
- Arrays of objects: merges fields across elements, marking a property required only when it is present in every element.
- Format detection (heuristic, optional): `date-time`, `date`, `email`, `uri`, `uuid`.
- Enum inference (optional): when a small set of string values repeats, they become an `enum`.
- `additionalProperties`: omit (validators default to true), set true, or set false.
- Copy button, dark-mode toggle, keyboard friendly (Ctrl or Cmd + Enter to generate).

## How it works

The tool parses your JSON with the browser's built-in `JSON.parse`, then walks the value tree. Objects become `{ "type": "object", "properties": ... }`, arrays become `{ "type": "array", "items": ... }`, and scalars map to the closest JSON Schema type (whole numbers become `integer`). For arrays and arrays of objects, the per-element schemas are merged: primitive types collapse into a union, and object properties are unioned with required tracking. String format and enum detection are heuristics you can switch off. No network requests are made.

## Privacy

Everything happens locally in your browser. Your JSON is never uploaded, logged, or sent anywhere. There are no external scripts, fonts, or stylesheets, so the page works offline. You can confirm by opening your browser DevTools and watching the network tab: no requests are made.

## License

MIT. Copyright 0xelitesystem 2026.
