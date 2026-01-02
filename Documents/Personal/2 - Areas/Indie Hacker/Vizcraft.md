# Vizcraft

## Scoping Decisions

**Out of scope (for now):**
- Multi-angle view
- Layer control
- StyleMagic + LumaLight combo

---

## Architecture Feedback

### Rendering Approach

Instead of having the LLM generate images directly (which is unreliable with dimensions), consider:

1. LLM reads the floor plan and converts it to **code/structured data** that represents exact dimensions
2. A custom library/compiler generates the final render from that structured format

### Proposed Format: `.vizmodel`

- LLM generates a JSON or proprietary format (`.vizmodel`) with all parameters and details
- The site processes this file through a compiler:
  ```bash
  vizcraft --input design_12062025.vizmodel --output render.png
  ```

### Benefits
- **More cost-effective**: Text generation is cheaper than image generation
- **Debuggable**: Can inspect and diff `.vizmodel` files to identify issues
- **Consistent**: Same parameters always produce same output (not random like LLM image generation)
- **Comparable**: Can compare how different models interpret the same input

### Reference Libraries (WebGL-based rendering)
- [blueprint3d](https://github.com/furnishup/blueprint3d)
- [blueprint-js](https://github.com/aalavandhaann/blueprint-js)

### Next Steps
- Explore building a custom WebGL library with descriptive API
- Train LLM on the custom library documentation
- Library provides assurance of consistent output from defined parameters
