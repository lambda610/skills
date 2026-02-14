# Complete Template Catalog

This document lists all built-in optimization templates from the prompt-optimizer project.

## Template Types Overview

| Type | English Name | Count |
|------|-------------|-------|
| User Prompt Optimization | userOptimize | 6 |
| System Prompt Optimization | optimize | 6 |
| Iteration | iterate | 3 |
| Text-to-Image | text2imageOptimize | 5 |
| Image-to-Image | image2imageOptimize | 3 |
| Evaluation | evaluation | 20+ |
| Variable Processing | variable | 2 |

---

## User Prompt Optimization (userOptimize)

### 1. Basic Optimization
- **Template Name**: Basic Optimization
- **Use Case**: Quick daily optimization, eliminate vague expressions, add key information
- **Trigger**: `optimize: xxx` or `basic: xxx`

### 2. Planning Optimization
- **Template Name**: Step-by-Step Planning
- **Use Case**: Complex tasks, break down vague requirements into actionable steps
- **Trigger**: `plan: xxx` or `stepwise: xxx`

### 3. Professional Optimization
- **Template Name**: Professional Optimization
- **Use Case**: Scenarios requiring precise descriptions, add quantifiable standards
- **Trigger**: `professional: xxx` or `pro: xxx`

### 4-6. Context Versions
- **Context Basic**: Minimum refinement with context constraints
- **Context Planning**: Plan with context into staged, trackable text
- **Context Professional**: Professionalize with context into executable and acceptable text

---

## System Prompt Optimization (optimize)

### 1. General Optimization
- **Template Name**: General Optimization
- **Use Case**: Most system prompts, restructure with standard format

### 2. Format Optimization
- **Template Name**: Format Optimization (Data Scenario)
- **Use Case**: Data analysis, report generation requiring structured output

### 3. Analytical Optimization
- **Template Name**: Analytical Optimization (Technical Scenario)
- **Use Case**: Code review, solution evaluation

### 4-6. Context Message Optimization
- **General Message**: General conversation scenarios
- **Context Analytical**: Technical scenarios
- **Context Format**: Data scenarios

---

## Iteration Optimization (iterate)

### 1. General Iteration
- **Template Name**: General Iteration
- **Use Case**: Improve existing prompts based on specific issues

### 2. Context Iteration
- **Template Name**: Context Iteration
- **Use Case**: Iteration with context and tool information

### 3. Image Iteration
- **Template Name**: Image Iteration (General)
- **Use Case**: Progressive image prompt iteration

---

## Text-to-Image Optimization (text2imageOptimize)

### 1. General Natural Language
- **Description**: Structured language for subject/action/environment/lighting/color/material/mood/composition

### 2. Chinese Aesthetic
- **Description**: Optimized for Chinese image generation models

### 3. Photography
- **Description**: Photography with emphasis on subject, composition, lighting, mood

### 4. Creative/Deconstructive
- **Description**: Deeply deconstruct text, create unique fantasy visuals

### 5. JSON Structured
- **Description**: Strict JSON output template

---

## Image-to-Image Optimization (image2imageOptimize)

### 1. General Image-to-Image
- **Description**: Natural language for restrained editing

### 2. Design Text Replacement
- **Description**: Keep layout, replace text only

### 3. JSON Structured
- **Description**: Strict JSON with extensible fields

---

## Prompt Evaluation (evaluation)

### By Mode

| Mode | Template | Description |
|------|----------|-------------|
| Original | Original Prompt Evaluation | Evaluate original prompt test results |
| Optimized | Optimized Prompt Evaluation | Evaluate optimized prompt effect |
| Comparison | Comparison Evaluation | Compare original vs optimized |
| Direct | Direct Evaluation | Direct quality evaluation |
| Iterative | Iterative Evaluation | Evaluate + improvement plan |

### By Prompt Type

- **System Prompt Evaluation**: Direct, Iterative
- **User Prompt Evaluation**: Direct, Iterative, Comparison
- **Multi-message Evaluation**: Original, Optimized, Comparison, Direct, Iterative
- **Variable Mode**: Original, Optimized, Comparison, Direct, Iterative
- **Image Prompt**: Text2Image Direct, Image2Image Direct

---

## Variable Processing

### 1. Variable Extraction
- **Template Name**: AI Intelligent Variable Extraction
- **Description**: LLM autonomously decides extraction granularity

### 2. Variable Value Generation
- **Template Name**: AI Intelligent Variable Value Generation
- **Description**: Infer variable values based on prompt context

---

## Trigger Keywords Quick Reference

| Function | Keywords |
|----------|----------|
| User Optimization | `optimize:`, `basic:`, `plan:`, `professional:` |
| System Optimization | `system prompt:`, `/system`, `format:`, `analytical:` |
| Iteration | `iterate:`, `improve:` |
| Text-to-Image | `/image`, `image:` |
| Image-to-Image | `image2image:`, `edit:` |
| Evaluation | `evaluate:`, `compare:` |
| Variables | `extract variables:`, `generate variables:` |
