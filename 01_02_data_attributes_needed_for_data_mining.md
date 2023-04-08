# Data attributes needed for data mining

## Knowledge check

1. Which statements are correct about attributes? Select all that apply.
   - The discrete attribute has only a finite or countably infinite set of values.
     - The real numbers belong to Continuous Attributes. Also, the Binary Attributes are a special case of discrete attributes.
   - The binary attributes are discrete attributes.
     - The real numbers belong to Continuous Attributes. Also, the Binary Attributes are a special case of discrete attributes.
2. Which attributes could contribute to data quality problems? Select all that apply.
   - Noise
     - Noise refers to the modification of original values.
   - Outliers
     - Outliers are data objects with characteristics that are considerably different than most of the other data objects in the data set.
   - Duplicate data
     - Missing values and duplicate data are intuitively critical to data quality.
   - Missing values
     - Missing values and duplicate data are intuitively critical to data quality.
3. What is the difference between “feature types or attributes” and “features or attribute values”?
   - Feature type or attributes are categories that express properties of data, while features or attribute values are actual numerical instances of the categories.
     - Feature type or attributes are categories that express properties of data, while features or attribute values are actual numerical instances of the categories.
4. True or False? Data sample IDs in dataset are used as an attribute
   - False
     - Typically, IDs are not useful attributes as they do not provide any specific information about the data sample.
5. For two points X = (3,7) and Y = (7,10), what would be the L1 and L2 norm?
   - 7, 5
     - L1 and L2 norm are Minkowski Distance with r equal to 1 and 2.
6. What is true about the curse of dimensionality? Select all that apply.
   - A large number of dimensions makes knowledge extraction slower
     - More dimensions do not imply more knowledge, because there can be dimensions that do not provide any insight on the data. This is called the Curse of Dimensionality.
   - A large number of dimensions can confuse knowledge extraction algorithms
     - More dimensions do not imply more knowledge, because there can be dimensions that do not provide any insight on the data. This is called the Curse of Dimensionality.
7. What is the difference between noise and outliers?
   - Noise is unwanted perturbations in the data for which there is a known reason while outliers are abnormalities in the data for which the reason is unknown and needs to be investigated.
     - Noise is unwanted, but outliers may tell something about the models.
8. What is true about Principal Component Analysis (PCA)? Select all that apply.
   - PCA focuses on dimensions with large amount of variation.
     - Amount of variation is used as importance measure in PCA.
   - PCA uses eigenvectors of the covariance matrix of data.
     - First covariance matrix of data is calculated, and then eigenvectors of this covariance matrix are found.
9. A data sample for a college student has the following four attributes: age, high school name, birth date, and rank in spelling competition.
   - Ratio, Nominal, Interval, Ordinal.
     - Nominal attributes have distinctness property, Ordinal attributes in addition have order property, Interval attributes also have addition property (they can be added or subtracted from each other), and Ratio attributes have the extra multiplication property on top of the other properties (they can be multiplied or divided to each other.
