# Applied ML

A common interview type is the "applied ML" interview, in which the intervier presents a product feature, and asks that you design an ML solution to implement the feature. These problems are usually given with minimal information or structure, and it is up to you to design a comprehensive solution. Consider the following two examples, which are taken from real interviews.

**Example 1:** How can we automatically identify posts on our feed that sell firearms?

**Example 2:** How can we predict the click-through rate (CTR) of an advertisement?

These are "solved" at the end of this note.

**What they are looking for:** The abilities to 1) translate ML methods into real-world products/outcomes, 2) quickly adjust to a domain you have probably never seen before, and 3) create structure (through exhaustive questioning) from a vauge outline.

## Approach

This is my usual approach to structuring an answer.

### Problem Design

1. Repeat the general (real-world) problem description back to the interviewer.
2. Identify who the key stakeholders are (users, clients, investors, citizens).
3. Identify domain-specific performance metrics.
4. Choose an ML problem (regression, classification, clustering, etc) that most closely resembles the applied problem, and confirm with your interviewer.

### Data Design

1. Identify the input and label spaces explicitly.
2. Determine how the training data is sampled/collected.
3. Ask if there is a feature engineering step, in which case suggest features relevant for the problem.
4. Ask if there are any privacy considerations that need to be taken into account.

### Modeling

1. Present a set of models that range from simple to complex. If there are images or text, use pretrained networks (ResNet50, BERT, more modern solutions, etc) to represent them as vectors, concatenate them with other numerical features for a combined representation. Then, apply linear or logistic regression to the output. In the simplest form, leave the encoders are frozen features and only solve the (convex) problem of learning the weights for the final layer. Then, add complexity by additionally adding one more layer to the head, or unfreezing the encoder weights and backpropagating through them. Note that you could also you a tree-based approach (see `tradeoffs.md`).
2. Identify all hyperparameters on the table (architecture, optimizers, encoders, etc).
3. Then, train the model and see if you successfully optimized the train loss. If not, options are to decrease the learning rate, or in some cases increase L2-regularization to upweight the strongly convex portion of the objective function. If you cannot optimize, there is not much use in discussing downstream performance.
4. Once the model is near-optimized, assess the generalization gap by checking validation loss. If there is one, make changes that aid generalization (i.e. regularization, model simplification). If there is no gap, but performance is not as good as it could be (discuss with your interviewer what this means), then increase model complexity.
5. In classication, after training a good model, consider optimizing the threshold to achieve a good balance of precision and recall. Discuss any other trade-offs in general.

### Deployment and Pitfalls

1. Consider deployment details, such as frequency of retraining, continuous updating, or centralized vs federated setup.
2. Mention issues of fairness, both in the abstract social sense and in the concrete technical sense (see [Agarwal (2018)](https://icml.cc/Conferences/2018/Schedule?showEvent=2361) for examples).
3. If not mentioned before, mention issues of class imbalance, which could cause a model selected based on accuracy perform badly at inference time.
4. If not mentioned before, this would also be a good place to discuss privacy concerns.
5. Most importantly, try to mention domain-specific pitfalls that can occur and need to be accounted for. For example, in Example 1 above, a Veteran's Day post might contain a firearm but not be selling it. Could this be a pitfall of the model, and can we correct for it?