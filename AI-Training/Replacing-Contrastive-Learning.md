# Perception & Prediction

<img width="1629" height="808" alt="image" src="https://github.com/user-attachments/assets/a41929f3-a3e7-41dc-8563-c618ad44e2e4" />


> A deep learning model contain 2 pieces:
> - Perception (Representation which help understanding the state of the world)
> - Prediction (task specific part which will reasoning/planing, make decision)
> 
> Reason why deep learning is also called "Representation Learning"

***

## How do we learn data representations?

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/65181ef8-60e0-4f7d-87d3-e9f1174ca31d" />


- Transfer from latent of the big models which is trained on a task that has large amount of data. But:
  - depend on relation between upstream task & downstream task
  - tricky on which layer to use & how to tune?
  - mostly for reducing amount of labeled data on the downstream task. Although upstream task has bottleneck on labeled data as well.

***

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/f031b4e3-b078-47a3-8d47-5af4e237d89e" />

- Leveraging self-supervised learning allows systems to learn directly from unlabeled data—making it easier to scale to massive datasets—while capturing foundational knowledge about the world through passive observation, much like a newborn infant.

***

<img width="2048" height="768" alt="image" src="https://github.com/user-attachments/assets/9765d5a0-0f39-4eb0-870a-d66f475ee3a2" />

- Some approaches for SSL: Energy-Based Model (EBM), along with Autoencoder models, and Autoregressive models

***

## Example of EBM:

### Siamese Net
<img width="713" height="344" alt="image" src="https://github.com/user-attachments/assets/b6e75aa6-e000-492b-b3b5-2c0a06508c70" />

### SimCLR (Simple Framework for Contrastive Learning of Visual Representations)
<img width="354" height="243" alt="image" src="https://github.com/user-attachments/assets/6d1ca429-5f1f-47a1-82d3-fea1b3048cee" />

### CLIP (Contrastive Language-Image Pre-training)
<img width="1600" height="973" alt="image" src="https://github.com/user-attachments/assets/9dd9526a-21e0-47ee-a5b3-4749d6b037e1" />


### JEPA (Joint Embedding Predictive Architecture)

<img width="815" height="193" alt="image" src="https://github.com/user-attachments/assets/11959088-8a5a-489f-9c03-77c3f4eb35da" />

## Training EBM:

#### Representation Collapsing problems

<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/21020ab4-b0c0-4bcd-a967-d602d2244780" />


#### Contrastive Method
<img width="1672" height="941" alt="image" src="https://github.com/user-attachments/assets/79b226cf-b0dd-4165-aaf1-16e4cfccacda" />

[Collapsing in Contrastive method](https://arxiv.org/pdf/2110.09348)

#### Regularized Method
| Method             | What does it control?  | Core idea                                                                       |
| ------------------ | ---------------------- | ------------------------------------------------------------------------------- |
| **Stop-gradient**  | Gradient flow          | Treat the target as fixed during the current backward pass                      |
| **EMA**            | Teacher updates        | Update the teacher slowly using a moving average of student weights             |
| **SIGReg**         | Embedding distribution | Explicitly regularize representations toward an isotropic Gaussian distribution |

***

**Stop-gradient**:

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/ebe37d01-7fba-4af6-8f38-b332828b0178" />

*** 

**EMA**

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/438e1240-5661-4bd1-96ca-0a5c813514ae" />

***

**SIGReg**

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/fb294fb3-1982-446f-b82d-a9287af5869e" />

<img width="834" height="283" alt="image" src="https://github.com/user-attachments/assets/11297445-2ce8-4c12-a12c-af6e0c9f1d27" />




# Apply to Biological KG ???

