# Procedural Model Quality Checklist

- The model has a recognizable silhouette from the gameplay camera.
- Primary forms read clearly before material or post-processing detail.
- Secondary detail supports the asset role: panels, trims, ridges, tubes, fins, sockets, decals, or emissive accents.
- Tertiary detail is visible at intended camera distance and does not create noise.
- Materials have purposeful contrast in roughness, metalness, color, emissive, or texture.
- Bevels, curves, and segment counts improve silhouette or highlight behavior.
- Repeated props use shared geometries/materials, instancing, or pools when practical.
- Visual mesh and gameplay collision/proxy are intentionally separated when needed.
- The factory returns named groups/meshes and keeps ownership/disposal clear.
- Renderer diagnostics are checked when triangles, materials, textures, or draw calls increase.
- Mobile screenshot still shows the asset as more than a primitive placeholder.
