# Storybook Generator

## Overview
This project creates visually appealing storybooks from images and dialogue text. It transforms regular images into a cartoon-like style and arranges them into a formatted PDF storybook with scenes and dialogues. The tool is perfect for creating visual narratives, comic books, or educational materials.

## Features
- **Image Cartoonization**: Transforms regular photos into cartoon-style images
- **Text Overlay**: Adds dialogue text to images with proper wrapping and formatting
- **PDF Generation**: Creates a professional layout with two scenes per page
- **Image Enhancement**: Applies contrast enhancement and sharpening to improve visual quality
- **Multi-scene Support**: Organizes images into logical scenes
- **Cover Page**: Option to add a custom cover page
- **Background**: Custom background for all pages
- **Signatures**: Rotates between multiple signature images across pages

## Requirements
- Python 3.9+
- Required packages:
  - opencv-python (cv2)
  - numpy
  - Pillow (PIL)
  - reportlab
  - pandas
  - tqdm

## Installation
```bash
pip install opencv-python numpy pillow reportlab pandas tqdm
```

## Project Structure
```
project/
├── CSV/
│   └── Dialogues_English.csv
├── Images/
│   ├── scene1_image1.jpeg
│   └── ...
├── Font/
│   └── Wigglye.ttf
├── Sign/
│   ├── Anup Signature.jpeg
│   └── ...
├── Background Image/
│   └── Background.jpg
├── Movie Poster/
│   └── Movie poster.jpg
└── Storybook_English.ipynb
```

## How It Works

### 1. Data Organization
The story data is organized as a dictionary with scene names as keys and lists of image tuples as values. Each image tuple contains:
- Scene ID
- Image ID
- Image path

### 2. Image Processing
Each image goes through multiple processing steps:
- Resizing and compression
- Enhancement with CLAHE (Contrast Limited Adaptive Histogram Equalization)
- Edge detection and sharpening for cartoon effect
- Text overlay with proper wrapping

### 3. Layout Generation
- Images are organized into rows (default: 3 images per row)
- Rows are stacked to create scene pages
- Scenes are arranged in the PDF with two scenes per page
- A dividing line separates the scenes

### 4. PDF Creation
- Optional cover page
- Background image for all pages
- Scene titles
- Rotating signatures

## Usage

1. Prepare your dialogue data in a CSV file with columns for Scene ID, Image ID, and Dialogue.
2. Organize your images in a folder structure.
3. Update the `story_data` dictionary in the code with your scene and image information.
4. Run the script to generate your storybook PDF.

```python
# Example usage
create_storybook(
    story_data, 
    font_path='Font/Wigglye.ttf', 
    bg_image_path='Background Image/Background.jpg',
    cover_image_path='Movie Poster/Movie poster.jpg',
    signature_paths=signature_paths
)
```

## Customization

### Font
Change the font by providing a different font file path:
```python
create_storybook(story_data, font_path='your_font.ttf')
```

### Images Per Row
Adjust the number of images per row in the `create_scene` function:
```python
create_scene(scene_data, images_per_row=2)  # Default is 3
```

### Image Processing Parameters
Modify the cartoonization effect by adjusting parameters:
```python
process_image(image_path, dialogue, k=2, blur=7, line=9)
```
- `k`: Compression factor (higher = smaller image)
- `blur`: Median blur value (higher = more blur)
- `line`: Line size for edge detection (higher = more detail)
