# NostalgIA: Old Photo Restoration with GANs and U-Net

Final degree project (Proyecto Fin de Grado) for the Software Engineering degree at ETSISI, Universidad Politécnica de Madrid. Graded 10/10. Madrid, June 2024.

## What it does

NostalgIA restores damaged old photographs. It focuses on three common defects found in old pictures:

- Black-and-white photos (color restoration)
- Tears and missing pieces
- Scratches and fold creases

Because real pairs of damaged/undamaged photos do not exist at scale, the project simulates each defect synthetically on clean images, producing the input/output pairs needed for supervised training.

## Approach

- **Dataset:** CelebA (~210,000 celebrity face images, 218x178x3), chosen because the target use case is restoring photos of people.
- **Synthetic damage pipeline:** grayscale conversion with the channel replicated three times, Perlin noise with two thresholds to simulate tears (dark center and white edge), and Perlin noise combined with the Canny method to draw realistic creases and scratches.
- **First approach, GAN:** a generator received the damaged image and reconstructed it, while a discriminator learned to tell real images from generated ones. Promising results on the black-and-white defect, but the model struggled with tears and scratches even after improvements such as a dropout layer in the discriminator.
- **Final approach, U-Net:** the damaged image goes in as input and the network must output the repaired image. This architecture produced satisfactory results and met the project goals.

## Repository contents

- `Unet_Git.ipynb` - final U-Net model (MSE loss), damage simulation, batch loading, training loop and model save/load.
- `NostalgIA_Gan_git_Color.ipynb` - earlier GAN experiments (generator, discriminator and combined model).
- `NostalgIA__Restauración_de_imágenes_antiguas_utilizando_redes_UNet RBO.pdf` - full project report (in Spanish), released under a Creative Commons BY-NC-SA 4.0 license.

## Tech stack

Python, TensorFlow/Keras, OpenCV, NumPy, Perlin noise (`noise`), Matplotlib. The notebooks were built to run on Google Colab with Google Drive mounted, and expect the CelebA images extracted under `/content/Celeb/img_align_celeba`.

## Author

Raúl Baeza Osuna. Project advisor: Alberto Díaz Álvarez.
