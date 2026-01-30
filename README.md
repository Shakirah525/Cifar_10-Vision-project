# Cifar_10-Vision-project
CIFAR-10 Image Recognition using Transfer Learning (ResNet50)


📌 Project Overview

The goal of this project was to move beyond basic image processing and implement Transfer Learning to solve a complex multi-class vision problem. By leveraging a pre-trained expert model (ResNet50), I developed a system capable of identifying objects in tiny, low-resolution color photos.

📊 The Dataset: CIFAR-10

Categories: 10 (Airplane, Automobile, Bird, Cat, Deer, Dog, Frog, Horse, Ship, Truck).

Format: $32 \times 32$ RGB color images.

Sampling Decision: For this project, I sampled 10,000 images for training. This was a strategic trade-off to balance hardware efficiency on Google Colab with a robust learning signal.

🧠 Technical Strategy: The "Expert Brain"

Instead of building a model from scratch, I used ResNet50 pre-trained on ImageNet weights.

1. Preprocessing Logic

I implemented the official resnet50.preprocess_input tool.

Reasoning: Unlike simple scaling, this tool centers colors to match the "expert" model's memory, ensuring the pre-trained weights remain effective for our new data.

2. Two-Phase Training

Phase 1 (Feature Extraction): I "froze" the expert brain and only trained a custom classification head. This ensured a stable start without "breaking" the expert weights.

Phase 2 (Fine-Tuning): I unfroze the expert and used a very low learning rate ($1e-5$). This allowed the model to "squint" and adjust to the tiny $32 \times 32$ resolution of the CIFAR-10 dataset.

📈 Key Insights & Results

The Accuracy Jump: My analysis showed a significant jump in performance immediately after unfreezing the base model in Phase 2.

Overfitting Control: To handle the small data size, I utilized a 50% Dropout layer as a safety net, forcing the model to learn shapes rather than just memorizing pixels.

Judgment: The model performs exceptionally well on animal categories but occasionally confuses Vehicles (Trucks vs. Automobiles) due to similar spatial features at low resolutions.

🛠️ Tools Used

Language: Python

Libraries: TensorFlow, Keras, Matplotlib, NumPy

Architecture: ResNet50 (Transfer Learning)

Environment: Google Colab (T4 GPU)

🏁 Conclusion

This project demonstrates Analytical Maturity by prioritizing logic and trade-offs over simple technical perfection. It proves that Transfer Learning is a powerful, efficient way to solve real-world vision problems even under hardware and data constraints.
