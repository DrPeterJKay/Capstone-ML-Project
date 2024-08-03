# Model Card

See the [example Google model cards](https://modelcards.withgoogle.com/model-reports) for inspiration. 

## Model Description

### Input:

Numeric. The following inputs are required:
- Grade Mean (%): Mean of all the grades upto the threshold (nominally 50% of the way through the course)
- Grade Standard Deviation (%): Standard Deviation of all the grades upto the threshold (nominally 50% of the way through the course)
- VLE Mean (-/day): Mean of the number of daily interactions with the VLE (Virtual Learning Environment) upto the threshold (nominally 50% of the way through the course)
- VLE Standard Deviation (-/day):  Standard Deviation of the number of daily interactions with the VLE upto the threshold (nominally 50% of the way through the course)

### Output:

A binary prediction if a student is likely to withdraw (1) or not (0)

### Model Architecture:

** Describe the model architecture you’ve used

## Performance

Give a summary graph or metrics of how the model performs. Remember to include how you are measuring the performance and what data you analysed it on. 

## Limitations

Outline the limitations of your model.

## Trade-offs

Outline any trade-offs of your model, such as any circumstances where the model exhibits performance issues. 
