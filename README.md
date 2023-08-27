# !After Detailer

This fork of After Detailer is meant to work with [my own version of wildcards](https://github.com/Cryptik-Rick/sd-webui-wildcards-ad). Please follow the install instructions there. However, it will still work without issues if wildcards is not installed.

!After Detailer is a extension for stable diffusion webui, similar to Detection Detailer, except it uses ultralytics instead of the mmdet.


## Options

| Model, Prompts                    |                                       |                                                   |
| --------------------------------- | ------------------------------------- | ------------------------------------------------- |
| ADetailer model                   | Determine what to detect.             | `None` = disable                                  |
| ADetailer prompt, negative prompt | Prompts and negative prompts to apply | If left blank, it will use the same as the input. |

| Detection                            |                                                                                              |     |
| ------------------------------------ | -------------------------------------------------------------------------------------------- | --- |
| Detection model confidence threshold | Only objects with a detection model confidence above this threshold are used for inpainting. |     |
| Mask min/max ratio                   | Only use masks whose area is between those ratios for the area of the entire image.          |     |

If you want to exclude objects in the background, try setting the min ratio to around `0.01`.

| Mask Preprocessing              |                                                                                                                                     |                                                                                         |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| Mask x, y offset                | Moves the mask horizontally and vertically by                                                                                       |                                                                                         |
| Mask erosion (-) / dilation (+) | Enlarge or reduce the detected mask.                                                                                                | [opencv example](https://docs.opencv.org/4.7.0/db/df6/tutorial_erosion_dilatation.html) |
| Mask merge mode                 | `None`: Inpaint each mask<br/>`Merge`: Merge all masks and inpaint<br/>`Merge and Invert`: Merge all masks and Invert, then inpaint |                                                                                         |

Applied in this order: x, y offset → erosion/dilation → merge/invert.

#### Inpainting

Each option corresponds to a corresponding option on the inpaint tab. Therefore, please refer to the inpaint tab for usage details on how to use each option.

## ControlNet Inpainting

You can use the ControlNet extension if you have ControlNet installed and ControlNet models.

Support `inpaint, scribble, lineart, openpose, tile` controlnet models. Once you choose a model, the preprocessor is set automatically. It works separately from the model set by the Controlnet extension.

## Advanced Options

API request example: [wiki/API](https://github.com/Bing-su/adetailer/wiki/API)

`ui-config.json` entries: [wiki/ui-config.json](https://github.com/Bing-su/adetailer/wiki/ui-config.json)

`[SEP], [SKIP]` tokens: [wiki/Advanced](https://github.com/Bing-su/adetailer/wiki/Advanced)

## Media

- 🎥 [Unleashing the Power of Adetailer: Perfecting Faces and More](https://www.youtube.com/watch?v=ZNcz4k5JCCo&t=531s)

## Model

| Model                 | Target                | mAP 50                        | mAP 50-95                     |
| --------------------- | --------------------- | ----------------------------- | ----------------------------- |
| face_yolov8n.pt       | 2D / realistic face   | 0.660                         | 0.366                         |
| face_yolov8s.pt       | 2D / realistic face   | 0.713                         | 0.404                         |
| hand_yolov8n.pt       | 2D / realistic hand   | 0.767                         | 0.505                         |
| person_yolov8n-seg.pt | 2D / realistic person | 0.782 (bbox)<br/>0.761 (mask) | 0.555 (bbox)<br/>0.460 (mask) |
| person_yolov8s-seg.pt | 2D / realistic person | 0.824 (bbox)<br/>0.809 (mask) | 0.605 (bbox)<br/>0.508 (mask) |
| mediapipe_face_full   | realistic face        | -                             | -                             |
| mediapipe_face_short  | realistic face        | -                             | -                             |
| mediapipe_face_mesh   | realistic face        | -                             | -                             |

The yolo models can be found on huggingface [Bingsu/adetailer](https://huggingface.co/Bingsu/adetailer).

### Additional Model

Put your [ultralytics](https://github.com/ultralytics/ultralytics) yolo model in `webui/models/adetailer`. The model name should end with `.pt` or `.pth`.

It must be a bbox detection or segment model and use all label.

## Example

![image](https://i.imgur.com/38RSxSO.png)
![image](https://i.imgur.com/2CYgjLx.png)

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/F1F1L7V2N)
