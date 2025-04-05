**OpenGL Buffers Cheat Sheet**
-Arnav Sinha
---

### 1. **Vertex Buffer Object (VBO)**
- **Purpose:** Stores vertex data (positions, colors, normals, etc.) in GPU memory.
- **Usage:**
```cpp
unsigned int VBO;
glGenBuffers(1, &VBO);                  // Generate buffer ID
glBindBuffer(GL_ARRAY_BUFFER, VBO);    // Bind buffer type
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW); // Copy data
```

### 2. **Element Buffer Object (EBO / IBO)**
- **Purpose:** Stores indices to reuse vertices (draw complex shapes efficiently).
- **Usage:**
```cpp
unsigned int EBO;
glGenBuffers(1, &EBO);
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, EBO);
glBufferData(GL_ELEMENT_ARRAY_BUFFER, sizeof(indices), indices, GL_STATIC_DRAW);
```

### 3. **Vertex Array Object (VAO)**
- **Purpose:** Stores vertex attribute configurations and VBO/EBO bindings.
- **Usage:**
```cpp
unsigned int VAO;
glGenVertexArrays(1, &VAO);
glBindVertexArray(VAO);  // Bind before VBO/EBO and attribute setup

// Setup VBO and attributes after binding VAO
glBindBuffer(GL_ARRAY_BUFFER, VBO);
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, stride, (void*)0);
glEnableVertexAttribArray(0);

// Optional: bind EBO too
```

### 4. **Drawing with Buffers**
- **Non-indexed:**
```cpp
glDrawArrays(GL_TRIANGLES, 0, vertexCount);
```
- **Indexed (with EBO):**
```cpp
glDrawElements(GL_TRIANGLES, indexCount, GL_UNSIGNED_INT, 0);
```

### 5. **Cleanup (Good Practice)**
```cpp
glDeleteVertexArrays(1, &VAO);
glDeleteBuffers(1, &VBO);
glDeleteBuffers(1, &EBO);
```

---

### Buffer Usage Hints
- `GL_STATIC_DRAW`: Data set once, used many times.
- `GL_DYNAMIC_DRAW`: Data set and changed frequently.
- `GL_STREAM_DRAW`: Data set once, used few times.

---

### Typical Order for Setup
```cpp
1. glGenVertexArrays()
2. glGenBuffers() for VBO (and EBO if needed)
3. glBindVertexArray()
4. glBindBuffer(GL_ARRAY_BUFFER)
5. glBufferData()
6. glVertexAttribPointer() + glEnableVertexAttribArray()
7. glBindBuffer(GL_ELEMENT_ARRAY_BUFFER) (if EBO used)
```

---


