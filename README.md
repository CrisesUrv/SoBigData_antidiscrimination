# AntiDiscrimination library

The antidiscrimination library is a software package to discover and prevent discrimination in data sets removing direct and/or indirect discrimination biases preserving data quality.
The antidiscrimination library has been developed by researches of the [CRISES](https://crises-deim.urv.cat/web/) group at the [Universitat Rovira i Virgili](http://www.urv.cat/en/) in Tarragona (Catalonia, Spain).

This library implements the discrimination prvention method proposed in the paper:
```
S. Hajian and J. Domingo-Ferrer,
A methodology for direct and indirect discrimination prevention in data mining,
IEEE Transactions on Knowledge and Data Engineering, Vol. 25, no. 7, pp. 1445-1459, Jun 2013
https://doi.org/10.1109/TKDE.2012.72
```
## Getting Started
The antidiscrimination library takes as input:
* A CSV file containing the data set to be protected
* min support and min confidence: to consider a rule a frequent rule
* alfa: discriminatory threshold to consider a frequent rule a direct or an indirect discrimination rule
* DI: Predetermined discriminatory items (attribute,discriminatory value)

### Prerequisites
* *The input dataset* is a CSV formatted file where each row corresponds to a record and each column corresponds to an attribute.
Within the CSV file, a first line (header) stating the name of the attributes is required. A sample dataset is provided in the 'input_datasets' folder.
* *The dataset configuration parameters* set the min_support, min_confidence, alfa and DI parameters described in the previous section.

The computer should fulfill the following requirements:
* Python v3.x must be installed. Python can be downloaded from: https://www.python.org/downloads/
* At least 8 GB of RAM are recommended.

### Code
The source code is available in this repository inside the ['src'](https://github.com/CrisesUrv/SoBigData_antidiscrimination/tree/master/src) folder.
The code is divided into four modules:
* *algorithms*: includes the antidiscrimination implementation algorithm
* *entities*: includes the entity classes supporting the algorithm
* *tests*: includes a python file with examples on how to use the API calls
* *utils*: includes different support classes and functions

The source code can be imported to python IDEs (e.g. Pycharm) by cloning or downloading the project from the [main page](https://github.com/CrisesUrv/SoBigData_antidiscrimination) on github.
The necessary python packages and its dependencies can be installed using the provided "requirements.txt" file as follows:
```
pip install -r requirements.txt
```
We recommend using a python environment for this project and install the necessary python packages on it.

### Running the antidiscrimination library example
In the root of the project, we have included a runnable python file named "anti_discrimination_test.py" that protects the example dataset from antidiscrimination.
Specifically, the example dataset consist of the Adult data set which is used very frequently for data mining tasks and it is available at: https://archive.ics.uci.edu/ml/datasets/adult 

To run the example file, access to the root folder and execute the following command from the console:
```
python anti_discrimination_test.py
```
A progress bar indicating the current and expected runtime will be shown.
The resulting protected dataset will be stored in the "output_datasets" directory, with the same name as the original dataset but with '_anom' suffix.
In addition, several metrics stating the information loss and discrimination risk resulting of the data transformation process are provided.

### API

The antidiscrimination library can be executed programmatically via the provided python API.
See below an example describing how to protect the provided example dataset through API calls

```
# Dataset loading
path_csv = "input_datasets/adult_anti_discrimination.csv"
data_frame = utils.read_dataframe_from_csv(path_csv)
dataset = Dataset_DataFrame(data_frame)

# Show a brief description of the data set
dataset.description()

# Set the anti discrimination parameters:
min_support = 0.02
min_confidence = 0.1
alfa = 1.0
DI = [("age","young"), ("sex","female")]
anonymization_scheme = Anti_discrimination(dataset, min_support, min_confidence, alfa, DI)

# Launch the direct and indirect anti discrimination process
anonymization_scheme.calculate_anonymization()

# Calculate and show discrimination metrics
anti_discrimination_metrics = anonymization_scheme.calculate_metrics()
anti_discrimination_metrics.description()

# Save the protected data set to disk in csv format"""
anonymization_scheme.save_anonymized_dataset("output_datasets/adult_anti_discrimination_anom.csv")

# The protected data set can be converted to pandas dataframe"""
df_anonymized = anonymization_scheme.anonymized_dataset_to_dataframe()
print(df_anonymized.head())
```

A complete example describing the API usage is available in the file "anti_discrimination_test.py" located inside the folder ['tests'](https://github.com/CrisesUrv/SoBigData_antidiscrimination/tree/master/src/tests)   

## Authors

Researchers of the [CRISES](https://crises-deim.urv.cat/web/) group of the [Universitat Rovira i Virgili](http://www.urv.cat/en/) in Tarragona (Catalonia).

## Resources

The algorithm implemented by the antidiscrimination library is detailed in the following publication.
The paper also contain theoretical and empirical analyses on a variety of use cases.

S. Hajian and J. Domingo-Ferrer,
[A methodology for direct and indirect discrimination prevention in data mining](https://doi.org/10.1109/TKDE.2012.72)
A methodology for direct and indirect discrimination prevention in data mining,
IEEE Transactions on Knowledge and Data Engineering, Vol. 25, no. 7, pp. 1445-1459, Jun 2013

## License

This project is licensed under the MIT License.
