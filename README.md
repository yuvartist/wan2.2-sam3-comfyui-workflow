# Wan 2.2 + SAM3 ComfyUI Workflow

A ComfyUI workflow for generating a short vertical Wan 2.2 image-to-video reaction clip, then using SAM3 to create a subject matte, transparent-character export, and green-screen export.

## Preview

The images below show the green-screen result, the original footage, and the subject mask. Add the three supplied images to `assets/` using these filenames to display them here:

| Green-screen export | Original footage | SAM3 subject mask |
| --- | --- | --- |
| ![Woman on green screen](assets/Wan22_green_screen_00004.png) | ![Original footage](assets/original.png) | ![SAM3 subject mask](assets/subject-mask.png) |

## Workflow

Open [`wan2.2_sam3.json`](wan2.2_sam3.json) in ComfyUI. The graph generates 65 frames at 432 × 768 (vertical 9:16) and defaults to 16 FPS. The prompt describes a restrained facial reaction followed by a late hibiscus appearance.

### Exports

- Original video (ComfyUI `SaveVideo` node)
- Black-and-white subject matte (ProRes HQ MOV)
- Transparent character (ProRes 4444 MOV)
- Green-screen composite (H.264 MP4)

### Requirements

Install ComfyUI and the custom nodes used by the workflow:

- [ComfyUI VideoHelperSuite](https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite)
- [ComfyUI-SAM3](https://github.com/PozzettiAndrea/ComfyUI-SAM3)

The graph expects the Wan 2.2 I2V high- and low-noise 14B models, `wan_2.1_vae.safetensors`, and the UMT5 XXL text encoder. Place model files in the appropriate ComfyUI model folders and ensure the SAM3 model is available to the SAM3 nodes. Model access and licensing are governed by their respective publishers.

### Before running

1. Load a flower-free starting image in the `LoadImage` node; the workflow JSON currently contains the original machine-specific filename.
2. Check that the model files and custom nodes are installed and recognized by ComfyUI.
3. Adjust the positive prompt, frame rate, output names, and SAM3 text prompt as needed.
4. Queue the workflow. The SAM3 branch processes the generated frames.

**Audio note:** The workflow includes an optional `LoadAudio` node, but it is not connected to the video assembly node in this JSON. Connect it to `CreateVideo` if you want the soundtrack included.

## Files

- `wan2.2_sam3.json` — ComfyUI workflow.
- `assets/` — preview images used above (add the three supplied images as `green-screen.png`, `original.png`, and `subject-mask.png`).

## Notes

The workflow stores ComfyUI node and model names, not the model weights or custom-node code. Output appearance and segmentation quality depend on the input image, model versions, prompts, and runtime setup.
