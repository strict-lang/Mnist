# Mnist
Handwritten digits for the neural networks of [Strict](https://github.com/strict-lang/Strict): small samples of the MNIST images (the ones AiInvest used) and two programs that learn them with the multilayer perceptron of the Strict `NeuralNetworks` package (`Dataset`, `Network`, `Layer`).

- `mnist/`: 160 PNG images with 16x16 gray pixels, the digits 0 to 3 (40 each), read with `ImageProcessing/Png` and `Compression/Inflate`.
- `mnist28/`: 280 JPG images with 28x28 gray pixels, the digits 4 to 9 (40 each, 60 of 8 and 9), read with `ImageProcessing/JpegPixels`.

Every fifth image is held out for testing, the others are trained in a new random order each epoch. The output layer is a softmax trained with cross entropy, the weights move with momentum 0.5.

| Program | Neurons | Epochs | Test accuracy | Native | Strict VM |
|---------|---------|--------|---------------|--------|-----------|
| `Digits.strict` | 256-32-4 | 100 | 100% of 32 images | 0.49 s | 58 s |
| `Digits28.strict` | 784-64-6 | 50 | 68-82% of 56 images | 2.8 s | |

Run them from this folder with `strict` of the Strict repository on the PATH (or `..\Strict\strict.exe`), the packages are found next to it: `strict Digits.strict` trains on the Strict VM, `strict build Digits.strict` builds `Digits.exe` and runs it. These are the first steps of the neural network use case of Strict, bigger networks and more images will show what parallel loops on all CPU cores, SIMD and the GPU bring.
