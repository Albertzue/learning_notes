1. Traditional learning processes build a new model for each new task, based on the available labeled data. This is because traditional machine learning algorithms assume training and test data come from the same feature space, and so if the data distribution changes, or the trained model is applied to a new dataset, users must retrain a newer model from scratch, even if attempting a similar task as the first model (e.g. sentiment analysis classifier of movie reviews versus song reviews). Transfer learning algorithms, however, takes already-trained models or networks as a starting point. It then applies that model’s knowledge gained in an initial source task or data (e.g. classifying movie reviews) towards a new, yet related, target task or data (e.g. classifying song reviews).

2. **multi-modal embedding model** is a type of foundation model that can processand understand both text and images.This
makes it suitable for powering a search application that handles queries containing both text and images.

3. **Text embedding model** This type of model is only designed to process text data, so it wouldn't be suitable for handling
image queries.
4. **Multi-modal generation model** This type of model is designed to generate text or images, not to search for them.
5. **Image generation model** This type of model is only designed to generate images, not to search for them.

### AWS Bedrock
6. **Temperature** This controls the randomness of the output, not the input prompt length.Temperature affects creativity, not
input size.
7. **Context window** This defines the maximum length of the input prompt the model can process. It directly limits how much
information can be included.
8. **Batch size** This is the number of prompts processed at once, affecting throughput, not individual prompt length. It's about processing multiple promptsefficiently.
9. **Model size** This relates to the model's overall capacity and complexity, not directly to the input prompt length. Size impacts performance, not input limits.
