---
title: WebGL2RenderingContext.drawElementsInstanced()
slug: Web/API/WebGL2RenderingContext/drawElementsInstanced
tags:
  - API
  - Method
  - Reference
  - WebGL
  - WebGL2
browser-compat: api.WebGL2RenderingContext.drawElementsInstanced
---
{{APIRef("WebGL")}}

The **`WebGL2RenderingContext.drawElementsInstanced()`** method
of the [WebGL 2 API](/en-US/docs/Web/API/WebGL_API) renders primitives from
array data like the {{domxref("WebGLRenderingContext.drawElements()",
  "gl.drawElements()")}} method. In addition, it can execute multiple instances of a set
of elements.

> **Note:** When using {{domxref("WebGLRenderingContext", "WebGL 1", "",
    1)}}, the {{domxref("ANGLE_instanced_arrays")}} extension can provide this method,
> too.

## Syntax

```js
void gl.drawElementsInstanced(mode, count, type, offset, instanceCount);
```

### Parameters

- `mode`

  - : A {{domxref("WebGL_API/Types", "GLenum")}} specifying the type primitive to render. Possible values
    are:

    - `gl.POINTS`: Draws a single dot.
    - `gl.LINE_STRIP`: Draws a straight line to the next vertex.
    - `gl.LINE_LOOP`: Draws a straight line to the next vertex, and
      connects the last vertex back to the first.
    - `gl.LINES`: Draws a line between a pair of vertices.
    - [`gl.TRIANGLE_STRIP`](https://en.wikipedia.org/wiki/Triangle_strip)
    - [`gl.TRIANGLE_FAN`](https://en.wikipedia.org/wiki/Triangle_fan)
    - `gl.TRIANGLES`: Draws a triangle for a group of three vertices.

- count
  - : A {{domxref("WebGL_API/Types", "GLsizei")}} specifying the number of elements to be rendered.
- type

  - : A {{domxref("WebGL_API/Types", "GLenum")}} specifying the type of the values in the element array
    buffer. Possible values are:

    - `gl.UNSIGNED_BYTE`
    - `gl.UNSIGNED_SHORT`
    - When using the {{domxref("OES_element_index_uint")}} extension:

      - `gl.UNSIGNED_INT`

- offset
  - : A {{domxref("WebGL_API/Types", "GLintptr")}} specifying an offset in the element array buffer. Must be
    a valid multiple of the size of the given `type`.
- instanceCount
  - : A {{domxref("WebGL_API/Types", "GLsizei")}} specifying the number of instances of the set of elements
    to execute.

### Return value

None.

### Exceptions

- If `mode` is not one of the accepted values, a
  `gl.INVALID_ENUM` error is thrown.
- If `offset` is a valid multiple of the size of the given type, a
  `gl.INVALID_OPERATION` error is thrown.
- If `count` or `instanceCount` are negative, a
  `gl.INVALID_VALUE` error is thrown.

## Examples

The following example shows how to draw multiple instances of a geometry with an index buffer.

> **Warning:** The following is educational, not production level code. It should generally be avoided to construct data / buffers within the rendering loop or right before use. 

```js
// binding the geometry buffer as usual
gl.bindBuffer(gl.ARRAY_BUFFER, geometryVertexBuffer);
gl.enableVertexAttribArray(vertexPositionAttributeLocation);
gl.vertexAttribPointer(vertexPositionAttributeLocation, 3, gl.FLOAT, false, 0, 0);

// binding the index buffer as usual
gl.bindBuffer(gl.ELEMENT_ARRAY_BUFFER, geometryIndexBuffer);

// build position buffer
const instancePositions = [];
for (const instance of instances) {
  instancePositions.push(
    instance.position.x,
    instance.position.y,
    instance.position.z
  );
}
const instancePositionBuffer = createWebGLBufferFromData(instancePositions);

// binding the instance positions buffer as you would with any attribute
gl.bindBuffer(gl.ARRAY_BUFFER, instancePositionBuffer);
gl.enableVertexAttribArray(instancePositionAttributeLocation);
gl.vertexAttribPointer(instancePositionAttributeLocation, 3, gl.FLOAT, false, 0, 0);

// mark the attribe as instanced and advance it every single(1) instance rather than every vertex
gl.vertexAttribDivisor(instancePositionAttributeLocation, 1);

// draw a geometry for each instance
gl.drawElementsInstanced(gl.TRIANGLES, 0, numGeometryVertices, 0, instances.length);
```


## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{domxref("WebGL2RenderingContext.drawArraysInstanced()")}}
- {{domxref("WebGL2RenderingContext.vertexAttribDivisor()")}}
- {{domxref("WebGLRenderingContext.drawArrays()")}}
- {{domxref("WebGLRenderingContext.drawElements()")}}
- {{domxref("ANGLE_instanced_arrays.drawArraysInstancedANGLE()")}}
- {{domxref("WEBGL_multi_draw.multiDrawElementsInstancedWEBGL()")}}
