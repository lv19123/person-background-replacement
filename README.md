# Person Background Replacement

Person Background Replacement — web application for replacing the background behind a person in images using a custom Mobile U-Net segmentation model.

The project demonstrates a practical computer vision pipeline: model training, person mask prediction, background replacement, CLI inference, and deployment as a Streamlit web app.

## Demo

**Live app:** [person-background-replacement Streamlit demo](https://person-background-replacement-4a4wyhoyvftepbrytn6xff.streamlit.app)

### Image Demo

Source image and replacement background:

![Source image and background](assets/readme_image0.png)

Image background replacement result:

![Image background replacement result](assets/readme_image1.png)

### Video Demo

Uploaded video and replacement background in the Streamlit app:

![Uploaded video and background in Streamlit app](assets/readme_video0.png)

Processed video result in the Streamlit app:

![Processed video result in Streamlit app](assets/readme_video1.png)

Processed demo video: [assets/output-video.mp4](assets/output-video.mp4)

## Features

- Person segmentation using Mobile U-Net
- Background replacement for uploaded images
- TensorFlow/Keras inference pipeline
- Streamlit web interface
- CLI inference for images
- CLI inference for videos
- Deployed on Streamlit Cloud

## Tech Stack

- Python
- TensorFlow / Keras
- OpenCV
- NumPy
- Pillow
- Streamlit

## Project Structure

```text
app_streamlit.py  - Streamlit web interface
src/              - model, losses, inference and video utilities
notebooks/        - training notebook
examples/         - sample input files
models/           - trained model
outputs/          - generated results
```

## Model

The project uses a Mobile U-Net style segmentation model with a MobileNetV2 encoder. The model is trained to predict a person mask, which is then used to composite the original person over a new background.

Expected model path:

```text
models/mobile_unet_model.keras
```

## How to Run Locally

```bash
pip install -r requirements.txt
streamlit run app_streamlit.py
```

## CLI Inference

Image inference:

```bash
python3 main_image.py \
  --image examples/test.jpg \
  --background examples/background.jpg \
  --model models/mobile_unet_model.keras \
  --output outputs/result_image.png \
  --mask-output outputs/mask_image.png
```

Video inference:

```bash
python3 main_video.py \
  --video examples/video.mp4 \
  --background examples/background.jpg \
  --model models/mobile_unet_model.keras \
  --output outputs/result_video.mp4 \
  --max-frames 120
```

## Training

The training workflow is stored in:

```text
notebooks/training.ipynb
```

It contains the model training process for person segmentation with a MobileNetV2 encoder and U-Net style decoder.

## Portfolio Note

This project is designed as a portfolio ML/CV project. It demonstrates the full computer vision workflow: training a segmentation model, running inference, replacing image and video backgrounds, building a web interface, and deploying the app to Streamlit Cloud.

## Notes

- A trained model file is required for inference.
- Large model files should be handled with Git LFS.
- Demo screenshots and the processed demo video are stored in `assets/`.
- Video inference is processed frame by frame, so longer videos can take more time.
