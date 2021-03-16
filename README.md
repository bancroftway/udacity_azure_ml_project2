# Operationalizing Machine Learning
This project utilizes Bank Marketing classification dataset. We utilize Azure AutoML to find the best performing model.
2 separate methods are utilized to operationalize the ML model:
1. An AutoML model is trained directly through the Python SDK. The best model is then exposed as a REST api endpoint.
2. A pipeline is used to perform AutoML training. The pipeline is exposed as a REST api endpoint. The best model is also exposed as a REST api endpoint.

The models are deployed through Azure Container Instance, and the REST api is secured using key based authentication. Swagger configuration for the REST endpoint is also exposed.

## Architectural Diagram
![Architectural Diagram](./screenshots/arch_diagram.PNG)

The Bank Marketing dataset is registered dataset, which can be used both directly in AutoML or in the Pipeline. An Azure AutoML model is trained, and deployed, and then this process is also further automated using a pipeline. The Pipeline takes care of finding or creating the registered dataset, and finding or creating the compute cluster, kicking off the AutoML experiment, retrieve the best model and deploy the model to a REST endpoint, through Azure Container Instance. Additionally, the model is secured using key based authentication, and logs output through Azure App Insights. Consumers of the model can interact with it using the REST endpoints. The Pipeline itself can be kicked off using a REST endpoint.

## Key Steps
1. We have registered the dataset in ML Studio. ![Image of Registered Dataset](./screenshots/s1.png)

2. Run AutoML experiment on compute cluster (classification with best model measured by accuracy metric). ![Completed Experiment](./screenshots/s2.png)

3. From all the models explored by AutoML, select the best-performing model. ![Image of Best Model](./screenshots/s3.png)

4. Deploy the best model as an endpoint with Azure Container Instance (ACI) ![Deployed Model](./screenshots/s4.png)

5. Enable logging (Application Insights) and view logs. ![Logging and insights](./screenshots/s5.png)

6. Download swagger.json from the deployed model endpoint, and display SwaggerUI locally, which shows the API methods available. ![Swagger](./screenshots/s6.png)

7. Using the deployed model endpoint, use the scoring endpoint. ![Endpoint](./screenshots/s7.png)

8. Use Apache Benchmark to benchmark the performance of the endpoint. ![Benchmark](./screenshots/s8.png)

9. Use Jupyter notebook to train and deploy an AutoML model as a pipeline. ![Pipeline](./screenshots/s9.png)

10. From the Pipeline node in ML Studio, we see the pipeline run has been completed. The Bank Marketing dataset is present and registered before being passed into the AutoML module. ![Running Pipeline](./screenshots/s10.png)

11. After waiting for the pipeline run to complete, it is is deployed as an endpoint. This REST endpoint can be invoked to trigger the pipeline 
a. The pipeline section of Azure ML studio, showing that the pipeline has been created  ![Finished Pipeline](./screenshots/s11a.png)

b. The pipelines section in Azure ML Studio, showing the Pipeline Endpoint ![Pipeline Endpoint](./screenshots/s11b.png)

c. The Bankmarketing dataset with the AutoML module ![Pipeline Run Execution](./screenshots/s11c.png)

d. The "Published Pipeline overview', showing a REST endpoint and a status of ACTIVE ![Notebook Rundetails](./screenshots/s11d.png)

e. In Jupyter Notebook, showing that the "Use RunDetails Widget" shows the step runs ![Pipeline Running from Endpoint](./screenshots/s11e.png)
f. In ML studio showing the scheduled run ![Pipeline Run](./screenshots/s11f.png)

## Screen Recording
https://youtu.be/zEQeMtZs7iU

## Improvements
In order to improve the model, we could employ deep learning, or increase the training time. Also, we note that the dataset is unbalanced i.e. there are far more 'no' values for the target 'y' column than there are 'yes' values. Additionally, the model could be improved by using multiple metrics instead of just one metric 'Accuracy'.
