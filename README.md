# Air-Quality-IoT-Analytics

### Introduction

Air pollution is a global problem and one of the most dangerous environmental risks to human health. In Europe, air quality remains poor in many cities that experience exceedances of the regulated limits for air pollutants. In this work, we present a real-world end-to-end air quality use case that leverages cutting-edge IoT devices and wireless technology to improve the living experience of citizens in urban areas. More particularly, we exploit the low-cost IoT devices to monitor air quality in multiple location points to build a historical air quality dataset that contains accurate (experts calibrated for precision close to air-quality stations) and reliable (resilient LoRa networks) concentrations of air pollutants. These data can be the foundation for European Environment Agency (EEA), World Health Organization (WHO), other e-government bodies to design ML algorithms for advanced air-quality analytics.

**[ipynb] Anomaly Detection using TRAFAIR Air Quality Dataset.ipynb**: We have run 12 unsupervised anomaly detection algorithms such as Angle-base Outlier Detection, Isolation Forest, clustering-Based Local Outlier, and other algorithms on the [TRAFAIR](https://www.dati.gov.it/view-dataset?Cerca=&tags_set=trafair&tags=trafair&ordinamento=&sort=Invia) air quality dataset. The anomaly score of each model type is provided along with the T-distributed Stochastic Neighbor Embedding (3D) and Uniform Manifold Approximation and Projection (2D) plots. 

**[html] Anomaly Detection using TRAFAIR Air Quality Dataset.html**: IPython notebook converted/exported to HTML.

Download the [html] file and open it via browser. The [ipynb] file can be loaded and viewed from the Github page, but it needs to be reloaded as the file is large. Hence, it is best to download and open via Google Colab or Jupyter Notebook.

### Air quality dataset build description

Numerous IoT devices are exploited to monitor and collect the pollution level on an urban scale in Modena, Florence, Pisa, Livorno, Santiago de Compostela, and Zaragoza (cities in Italy and Spain). As shown below, 14 IoT devices are installed in 12 points of Modena, Italy (similar installation in remaining cities). We show the installed device's hardware view in the same Figure below, where each device contains 4 cells (sensors), one for each gas (NO, NO2, CO, and Ox). Each cell measures the gas level through 2 channels (the auxiliary and the working channels) and provides a measure for each gas and channel in millivolts (mV). 

<img src="https://github.com/bharathsudharsan/Air-Quality-IoT-Analytics/blob/main/hardware_location.png" align="center" width="80%" height="80%">

### Unsupervised anomaly detection models

The accuracy of raw measurements by sensors is affected by events such as low battery voltage, weather conditions, air humidity, physical disturbances, and others. Since such events are prevalent in real-world distributed sensor deployment-based data collection practice, after data acquisition at the LoRa servers, we need to centrally run algorithms to identify and remove such abnormal data patterns.

The following anomaly detection models are created using PyCaret and trained using a part of the TRAFAIR dataset. 

![alt text](https://github.com/bharathsudharsan/Air-Quality-IoT-Analytics/blob/main/model_names.PNG)

### Assign anomaly labels to dataset

The data collection started in August 2019. The data rows generated by IoT devices contain sensor measurements, temperature, humidity, the battery voltage values with timestamps. These data rows are encapsulated into LoRa packets at the device level and sent to the LoRaWAN server via gateways.

The two columns 'Anomaly' and 'Anomaly_Score are added towards the end. 0 stands for inliers and 1 for outliers/anomalies. The score is the values computed by the algorithm. Outliers are assigned with larger anomaly scores.

![alt text](https://github.com/bharathsudharsan/Air-Quality-IoT-Analytics/blob/main/assign_a_model.PNG)

### Uniform manifold approximation and projection (umap) for outliers

Plot that can be used to analyze the anomaly detection model over different aspects. We provide users the freedom to use any model of their choice to detect and remove anomalies (due to events such as low battery voltage, physical disturbances, etc). The output is clean data that can power advanced air quality analytics tasks.

**How to remove the anomalies (yellow points)**: Just run the above trained unsupervised anomaly detection model of choice. Then, remove the data rows that correspond to high anomaly scores (set a threshold).

![alt text](https://github.com/bharathsudharsan/Air-Quality-IoT-Analytics/blob/main/umap_plot_for_outliers.png)

### Air quality data analytics

The battle against air pollution will be won with data. Following are few potential applications of the built dataset; (i) Train ML algorithms that can be centrally deployed (on a cloud platform) and give access to various APIs for forecasting/predicting (model inference) urban air quality in any given location point of Spain and Italy; (ii) Generate air quality index heat-map of past, present, future to rank the area's emission levels and track changes; (iii) Assessment, intervention, and use for e-government decision support (since reliable historic data) when forming pollution-reducing policies.

**Note**: In the [html] and [ipynb] files, the interactable plots are broken due to the high-resolution output by Plotly. It will appear back when the notebook is run again from start.

**If the code is useful, please consider citing paper using the BibTex entry below.**

```
@inproceedings{federica2021ubicomp,
  title={Air Quality Sensor Network Data Acquisition, Cleaning, Visualization, and Analytics: A Real-world IoT Use Case},
  author={Rollo, Federica and Sudharsan, Bharath and Po, Laura and Breslin, John G},
  booktitle={The ACM international joint conference on pervasive and ubiquitous computing (UbiComp)},
  year={2021}
}

@inproceedings{sudharsan2021iotdidemo,
  title={Demo abstract: Porting and execution of anomalies detection models on embedded systems in iot},
  author={Sudharsan, Bharath and Patel, Pankesh and Wahid, Abdul and Yahya, Muhammad and Breslin, John G and Ali, Muhammad Intizar},
  booktitle={International Conference on Internet-of-Things Design and Implementation (IoTDI)},
  year={2021}
}