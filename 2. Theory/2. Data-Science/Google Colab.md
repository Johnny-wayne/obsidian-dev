
**Colab** usa [[Jupyter Notebooks]] para rodar, ele aparenta ser totalmente baseado nisso, por isso o python. Apenas fazendo o host, a hospedagem desses *notebooks*.

Entre suas aplicações práticas, estão:

#### [[Data-Science]]

With Colab you can harness the full power of popular Python libraries to analyze and visualize data. The code cell below uses **[[Numpy]]** to generate some random data, and uses **[[matplotlib]]** to visualize it. To edit the code, just click the cell and start editing.


```python

import numpy as np
import IPython.display as display
from matplotlib import pyplot as plt
import io
import base64

ys = 199 + np.random.randn(100)
x = [x for x in range(len(ys))]

fig = plt.figure(figsize=(4, 3), facecolor='w')
plt.plot(x, ys, '-')
plt.fill_between(x, ys, 195, where=(ys > 195), facecolor='g', alpha=0.6)
plt.title("Sample Visualization", fontsize=10)

data = io.BytesIO()
plt.savefig(data)
image = F"data:image/png;base64,{base64.b64encode(data.getvalue()).decode()}"
alt = "Sample Visualization"
display.display(display.Markdown(F"""![{alt}]({image})"""))
plt.close(fig)
```

Output:
![[Pasted image 20240511171742.png]]•


---

You can import your own data into Colab notebooks from your Google Drive account, including from spreadsheets, as well as from Github and many other sources. To learn more about importing data, and how Colab can be used for data science, see the links below under [Working with Data](https://colab.research.google.com/#working-with-data).


---
#### [[Machine Learning]],

With Colab you can import an image dataset, train an image classifier on it, and evaluate the model, all in just [a few lines of code](https://colab.research.google.com/github/tensorflow/docs/blob/master/site/en/tutorials/quickstart/beginner.ipynb). Colab notebooks execute code on *Google's cloud* servers, meaning you can leverage the power of *Google hardware*, including [GPUs and TPUs](https://colab.research.google.com/#using-accelerated-hardware), regardless of the power of your machine. ==All you need is a browser.==

Colab is used extensively in the machine learning community with applications including:

- Getting started with [[TensorFlow]]
- Developing and training neural networks
- Experimenting with [[2. Theory/5. Generic/Hardware/TPUs - Tensor Processing Unit]]
- Disseminating AI research
- Creating tutorials

To see sample Colab notebooks that demonstrate machine learning applications, see the [machine learning examples](https://colab.research.google.com/#machine-learning-examples) below.

---

## More Resources

### Working with Notebooks in Colab

- [Overview of Colab](https://colab.research.google.com/notebooks/basic_features_overview.ipynb)
- [Guide to Markdown](https://colab.research.google.com/notebooks/markdown_guide.ipynb)
- [Importing libraries and installing dependencies](https://colab.research.google.com/notebooks/snippets/importing_libraries.ipynb)
- [Saving and loading notebooks in GitHub](https://colab.research.google.com/github/googlecolab/colabtools/blob/main/notebooks/colab-github-demo.ipynb)
- [Interactive forms](https://colab.research.google.com/notebooks/forms.ipynb)
- [Interactive widgets](https://colab.research.google.com/notebooks/widgets.ipynb)

### Working with Data

- [Loading data: Drive, Sheets, and Google Cloud Storage](https://colab.research.google.com/notebooks/io.ipynb)
- [Charts: visualizing data](https://colab.research.google.com/notebooks/charts.ipynb)
- [Getting started with BigQuery](https://colab.research.google.com/notebooks/bigquery.ipynb)

### Machine Learning Crash Course

These are a few of the notebooks from Google's online Machine Learning course. See the [full course website](https://developers.google.com/machine-learning/crash-course/) for more.

- [Intro to Pandas DataFrame](https://colab.research.google.com/github/google/eng-edu/blob/main/ml/cc/exercises/pandas_dataframe_ultraquick_tutorial.ipynb)
- [Linear regression with tf.keras using synthetic data](https://colab.research.google.com/github/google/eng-edu/blob/main/ml/cc/exercises/linear_regression_with_synthetic_data.ipynb)

### Using Accelerated Hardware

- [TensorFlow with GPUs](https://colab.research.google.com/notebooks/gpu.ipynb)
- [TensorFlow with TPUs](https://colab.research.google.com/notebooks/tpu.ipynb)

---
### Featured examples

- [NeMo Voice Swap](https://colab.research.google.com/github/NVIDIA/NeMo/blob/stable/tutorials/VoiceSwapSample.ipynb): Use Nvidia's NeMo conversational AI Toolkit to swap a voice in an audio fragment with a computer generated one.
    
- [Retraining an Image Classifier](https://tensorflow.org/hub/tutorials/tf2_image_retraining): Build a Keras model on top of a pre-trained image classifier to distinguish flowers.
    
- [Text Classification](https://tensorflow.org/hub/tutorials/tf2_text_classification): Classify IMDB movie reviews as either _positive_ or _negative_.
    
- [Style Transfer](https://tensorflow.org/hub/tutorials/tf2_arbitrary_image_stylization): Use deep learning to transfer style between images.
    
- [Multilingual Universal Sentence Encoder Q&A](https://tensorflow.org/hub/tutorials/retrieval_with_tf_hub_universal_encoder_qa): Use a machine learning model to answer questions from the SQuAD dataset.
    
- [Video Interpolation](https://tensorflow.org/hub/tutorials/tweening_conv3d): Predict what happened in a video between the first and the last frame