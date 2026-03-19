# Semantic Image Editing with DINOv3 + Gemini

A hackathon proof of concept for selection-based image editing that runs entirely in the browser as a single HTML file.

The idea: use DINOv3's dense feature similarity to **semantically select** a subject, crop it out with a feather mask, send **only that region** to Gemini for editing, then composite the result back into the original position -- without the model ever seeing or touching the rest of the image.

> [!NOTE]
> This is forked from my older hackathon submission. The approach is already outdated -- newer models handle localized editing natively, making this a good example of [the bitter lesson](http://www.incompleteideas.net/IncIdeas/BitterLesson.html): clever pipelines built around model limitations will eventually be replaced by simply making the models better.

## What Was Already There

The base project is the [DINOv3 Web](https://huggingface.co/spaces/webml-community/dinov3-web) HuggingFace Space by the ONNX Community -- a feature extraction viewer that runs DINOv3 inference in the browser via WebGPU (with WASM fallback) and visualizes patch similarity on hover.

## What I Added

- **Additive / subtractive selection** -- click to build up or refine a selection using positive and negative patches
- **Real-time threshold slider** -- control which patches pass the activation threshold for export
- **Feather mask & crop** -- extract the selected region as a masked, cropped canvas
- **Gemini round-trip** -- send the crop to `gemini-2.5-flash-image` with a text prompt, receive the edit back, and composite it into the original position
- **Multi-stage editing** -- each edit is baked into the original, enabling sequential edits

## Known Limitations

Built under a 48-hour time constraint:
- Selection breaks if scale ≠ 1.0
- Export selection button is non-functional (the Gemini send button handles this)

## More Info

<!-- Replace LINK with your actual Kaggle URL -->
See the [writeup on Kaggle](https://www.kaggle.com/competitions/banana/writeups/dino-banana-surgical-image-editing) for details, motivation, and results.

## License

Apache-2.0
