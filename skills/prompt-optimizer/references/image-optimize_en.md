# Image Optimization

Text-to-image and image-to-image prompt optimization.

## Text-to-Image Optimization (text2imageOptimize)

### 1. General Natural Language

**Use Case**: Most image generation needs

**Trigger**:
```
/image a cat
image: futuristic city
```

---

### 2. Chinese Aesthetic

**Use Case**: Chinese context and cultural elements

**Trigger**:
```
/image Chinese landscape painting
image: ancient Chinese beauty
```

---

### 3. Photography

**Use Case**: Photography-style image generation

**Trigger**:
```
/image portrait photography
image: night cityscape
```

---

### 4. Creative/Deconstructive

**Use Case**: Creative, fantasy, unique styles

**Trigger**:
```
/image creative: dream
creative: abstract art
```

---

### 5. JSON Structured

**Use Case**: Need structured output for image prompts

**Trigger**:
```
/image JSON: cat
image structured: city
```

---

## Image-to-Image Optimization (image2imageOptimize)

### 1. General Image-to-Image

**Use Case**: Image editing, modification

**Trigger**:
```
image2image: change background to night
edit: add border
```

### 2. Design Text Replacement

**Use Case**: Keep layout, replace text only

### 3. JSON Structured

**Use Case**: Precise control for image-to-image

---

## Image Iteration (imageIterate)

### General Iteration

**Use Case**: Progressive improvement based on previous results

**Trigger**:
```
image iterate: make the cat cuter
iterate: add more lighting effects
```

---

## Usage Examples

### Example 1: Text-to-Image

**Original**:
> a cat

**Optimized**:
> A cute British Shorthair cat, round face with large eyes, silver-gray fur, soft and smooth. Sitting on an antique wooden cabinet, sunlight streams in from the left window, casting warm light on the table. Background shows blurred bookshelves and a desk lamp, creating a warm home atmosphere. Cinematic portrait photography style, depth of field effect to highlight the subject.

---

### Example 2: Photography

**Original**:
> city night view

**Optimized**:
> Shanghai Lujiazui night scene, skyscrapers with bright lights, Oriental Pearl Tower standing in the center. Wet streets after rain reflect neon lights, traffic streams forming light trails. Cyberpunk futuristic vibe, blue and orange light interweaving. Wide-angle lens, 30-second long exposure, shot on tripod.
