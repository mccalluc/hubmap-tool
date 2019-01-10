# hubmap-tool

New requested features:
- Given a set, color it. / name it
- Recover the query, bounding rect that defined a subset (future)
- Spatial component is given colors for each cell: (it’s possible for a cell not to have a color)
  - Might be classification,  (palette, and names)
  - or might be expression levels.
- Separate events for genes and molecules coming from spatial.

Architecture:
- Global state not seen as a good thing: we want to decouple the components
- ... so each component may have its own, redundant copy of the cell or gene data: We might actually use the same data structure for each of them, but that’s not an assumption we want to build on.

Choices:
- Mobx?
- PubsubJS?
- Redux?

Usually when I think of an API, it’s centered on methods and their interfaces, but here it sounds like we want to instead identify events and the data they carry.

Scope:
- We are not discussing window management, resizing, etc.
- We are not discussing actions internal to a tool… ie, panning the spatial view, or mouse position in tSNE, but it may be that we do want to publish more, eventually.

## Spatial
### Publish
### Subscribe
These events will populate the tool:

```
AddCells({
  "cell-42": {
    "boundary": [[1234, 2345], [1235, 2366], ...], 
    ...
  },
  ...
})

AddMolecules({
  "molecule-42": {
    "gene_id": "gene-42",
    "position": [1234, 2345]
  },
  ...
})

AddRGBImagery({
  "name": "Interesting stain",
  "imagery": [
    [[r, g, b], [r, g, b], ...],
    [[r, g, b], [r, g, b], ...],
    ....
  ]
})
```

