# Сегментация человека и замена фона

Streamlit-приложение для сегментации человека и замены фона на изображениях и видео. Проект использует модель сегментации в стиле Mobile U-Net с энкодером MobileNetV2: модель предсказывает маску человека, после чего исходный фон заменяется на изображение, выбранное пользователем.

Репозиторий включает ноутбук с обучением модели, переиспользуемые функции инференса, CLI-интерфейсы для обработки изображений и видео, а также интерактивный веб-интерфейс на Streamlit.

## Демо

### Демо для изображения

Исходное изображение и новый фон:

![Исходное изображение и фон](assets/readme_image0.png)

Результат замены фона на изображении:

![Результат замены фона на изображении](assets/readme_image1.png)

### Демо для видео

Загруженное видео и фон в Streamlit-приложении:

![Загруженное видео и фон в Streamlit-приложении](assets/readme_video0.png)

Результат обработки видео в Streamlit-приложении:

![Результат обработки видео в Streamlit-приложении](assets/readme_video1.png)

Готовое демо-видео: [assets/output-video.mp4](assets/output-video.mp4)

## Возможности

- Сегментация человека
- Замена фона на изображениях
- Замена фона на видео
- Веб-интерфейс на Streamlit
- CLI-инференс для изображений
- CLI-инференс для видео

## Стек технологий

- Python
- TensorFlow / Keras
- MobileNetV2
- U-Net style decoder
- OpenCV
- NumPy
- Streamlit
- Albumentations
- scikit-learn
- Matplotlib
- Pandas

## Структура проекта

```text
.
├── app_streamlit.py          # Streamlit-приложение
├── main_image.py             # CLI для замены фона на изображениях
├── main_video.py             # CLI для замены фона на видео
├── src/
│   ├── inference.py          # Инференс для изображений, маски и сохранение результатов
│   ├── video.py              # Покадровая обработка видео
│   ├── model.py              # Архитектура Mobile U-Net / MobileNetV2
│   ├── losses.py             # Пользовательские loss-функции и метрики
│   └── __init__.py
├── notebooks/
│   └── training.ipynb        # Обучение модели
├── examples/                 # Примеры входных изображений, фона и видео
├── assets/                   # Демо-материалы для README
├── models/                   # Ожидаемое расположение обученной модели
├── outputs/                  # Результаты инференса
├── requirements.txt
├── .gitignore
└── README.md
```

## Модель

Для инференса требуется файл обученной модели. Большие файлы модели игнорируются через `.gitignore`, поэтому обученная модель не должна храниться в GitHub-репозитории.

Ожидаемый путь к обученной Keras-модели:

```text
models/mobile_unet_model.keras
```

## Установка

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Запуск Streamlit-приложения

```bash
python -m streamlit run app_streamlit.py
```

В приложении доступны две вкладки:

- `Image` для загрузки исходного изображения и нового фона
- `Video` для загрузки исходного видео и нового фона

## Инференс для изображения

Пример запуска замены фона на изображении из командной строки:

```bash
python3 main_image.py \
  --image examples/test.jpg \
  --background examples/background.jpg \
  --model models/mobile_unet_model.keras \
  --output outputs/result_image.png \
  --mask-output outputs/mask_image.png
```

## Инференс для видео

Пример запуска замены фона на видео из командной строки:

```bash
python3 main_video.py \
  --video examples/video.mp4 \
  --background examples/background.jpg \
  --model models/mobile_unet_model.keras \
  --output outputs/result_video.mp4 \
  --max-frames 120
```

Параметр `--max-frames` удобно использовать для быстрых тестов. Если его не указывать, будет обработано всё видео.

## Обучение

Обучение модели находится в ноутбуке:

```text
notebooks/training.ipynb
```

Ноутбук содержит workflow обучения модели сегментации человека на основе Mobile U-Net / MobileNetV2.

## Примечания

- Для инференса нужен файл обученной модели.
- Большие файлы модели не добавляются в GitHub.
- Демо-материалы хранятся в `assets/`.
- Инференс видео выполняется покадрово, поэтому обработка длинных видео может занимать заметное время.

## TODO

- Улучшить качество сегментации
- Добавить больше примеров
- Подготовить деплой
- Оптимизировать инференс видео
