# Perception & Prediction

<img width="1629" height="808" alt="image" src="https://github.com/user-attachments/assets/a41929f3-a3e7-41dc-8563-c618ad44e2e4" />


> A deep learning model contain 2 pieces:
> - Perception (Representation which help understanding the state of the world)
> - Prediction (task specific part which will reasoning/planing, make decision)
> 
> Reason why deep learning is also called "Representation Learning"

## Foundation Model, World Model
- Approaches to learn representation of a World Model:
  - Transfer from latent of the big models which is trained on a task that has large amount of data. But:
    - depend on relation between upstream task & downstream task
    - tricky on which layer to use & how to tune?
    - mostly for reducing amount of labeled data on the downstream task. Although upstream task has limit labeled data as well.
  - Use Self-supervised Learning and learn directly from unlabeled data (easier to scale to large amount of data). Also help capturing knowledge about "world" just by observe (similar to new born human) -> One approach is Energy Based Model (EBM) along side with Auto-encoder model, Autoregressive model
- Overview about EBM and introduce to some models:
  - Siamese Net
  - SimCLR
- Architecture of EBM:
  - Joint Embedding Architecture
  - Joint Embedding Predictive Architecture
- Embedding Collapsed problem
- Approaches to train an EBM
  - Contrastive Learning with downside of Negative Sampling
  - JEPA with Regularization
    - Stop-gradient (I-JEPA)
    - Teacher Target (I-JEPA)
    - EMA (I-JEPA)
    - SigReg (LeJEPA)





# SSL

## Contrastive Learning

### Siamese Net
<img width="713" height="344" alt="image" src="https://github.com/user-attachments/assets/b6e75aa6-e000-492b-b3b5-2c0a06508c70" />

### SimCLR
<img width="354" height="243" alt="image" src="https://github.com/user-attachments/assets/6d1ca429-5f1f-47a1-82d3-fea1b3048cee" />

### Joint Embedding Models

<img width="815" height="193" alt="image" src="https://github.com/user-attachments/assets/11959088-8a5a-489f-9c03-77c3f4eb35da" />
