# Data-Science-CSI-edition
Mandatory project in subject "Introduction to Data Science" which goal is to analyze and study behaviours in data of offences against property. Buyout clause 1 million dollars.

Data: https://opendata.smit.ee/ppa/csv/vara_2.csv

Data description: https://www2.politsei.ee/dotAsset/802507.pdf?fbclid=IwAR1o0yKNK60gK9udtuSzwDMnRNf8VtIDCDRFKG4MKclh2RIr3kT80yEsFyE

[Project slide](https://docs.google.com/presentation/d/1RHDUPsJVVtwVfPp8-WxsK8udEpYOmf4Ki9NjtbgpLDU/edit#slide=id.g48274606ac_250_0)

Task 1. Business understanding

Identifying your business goals
Background
The project is made for a data mining course. Real world application would be for police forces.
In Estonia, the lack of resources for the police is a rather common topic and known problem. Crimes often go unsolved. However, with limited resources the effectiveness can be still be increased by using them more effectively.
Decreasing the number of crimes and their severity can also be accomplished by better informing people on how to act during a crime or how to report it and how to decrease the chance of something happening to them (for example, how to better secure your car against theft).
This project only covers property crimes.
Business goals
More effective distribution of forces and resources and crime prevention, i.e. decreased total losses, decreased number of property crimes. Prioritize crimes based on the expected loss to have better response time and solve rate for more serious crimes.
(The police as the employer is only theoretical)
Business success criteria
Crime rates would drop if our finding were used to improve police work. Also more high loss cases would be solved.
Assessing your situation
Inventory of resources
Three beginner data scientists, some computers, python with relevant libraries, data about property crimes in Estonia during the five last years (2013 - 2017). 
Data is licensed under Creative Commons 3.0, which means the data can be freely shared and manipulated as long as appropriate credit is provided and any changes done to the data have been reported.
Requirements, assumptions, and constraints
The data is publicly available. The project needs to be finished by December 17
Risks and contingencies
Lack of time to work on the project - will result in worse results or other team members having to do more.
Terminology
Property crime (varavastane süütegu) - crimes that cause loss or damage of property against the owners will.
Süütegu - karistusseadustik sätestab, et süüteod jagunevad kuritegudeks ja väärtegudeks. Kuritegu kahjustab ohvri õigushüve, samas kui väärtegu kujutab endast pisemate rikkumiste menetlemist. Piir väärteo ja kuriteo vahel on 200 eurot.
Costs and benefits
Costs: 3 * 24h of (unpaid) work.
Benefits: up to 20 more points for data science course. Possibility for the police to improve their work.
Defining your data-mining goals
Data-mining goals
Visualize the frequency of different property crime types relative to the population for every county.
Train a model to predict the loss of a crime (a categorical range value with 4 different ranges).
Data-mining success criteria
We have a visualization of crime frequencies on the Estonian map.
We have trained a model to predict the loss of a property crime with accuracy of 0.9, precision 0.5, recall 0.5.
We have trained a model which helps to prioritise crimes according to their seriousity (damage costs) with AUC score of 0.75. 

Task 2. Data understanding

Gathering data
Outline data requirements
Data should be freely accessible and shareable. Work and data should be allowed to be published or at least to be used for educational purposes.
Verify data availability 
Data [1] is accessible under Creative Commons 3.0. Data has also been duplicated onto the team members’ computers in case the original source becomes unavailable.
Define selection criteria
The data will be provided by the Estonian Open Government Data Portal[3]. More specifically [1] will be used, which is a comma-separated values (csv) file, roughly 43 MB of size. The data is not holistic, bits and pieces are missing here and there. We will keep all of the fields for now.
Describing data
The csv file contains 125867 lines of data and possibly 27 features for each line. First column has the unique ID for the crime committed. Columns 2-6 include data about the date, start and end time, day of the week - everything related to the time of the crime. Columns 7 and 8 include data about the type of crime.  Column 8 and 9 are include info about the type of crime and whether or not the crime scene at hand was monitored in any way. Features 10-15 are about which laws were violated. Column 16 contain information about cost / damages done. Column 17 till 23 are all about location starting from the most abstract location identification and finishing with location coordinates.  24-26 contain vehicle information - type, model, year. Last column is about which type of crime it was. 
Exploring data
CaseId is a string of hex numbers, segmented into lengths 8,4,4,4,13 and stringed together with hyphens. Several instances of same unique IDs may be present in the data set when several crimes/misdemeanors correspond to the same event.
Beginning date (when the crime started) is of type string in the format of YYYY-MM-DD. 
Beginning time is in the format of HH:MM, also a string. Start of the crime period.
Day of the week when the crime was committed is in a form of a string, containing special alphabetical characters unique to Estonian language, e.g. Pühapäev.

End date (when the crime is reported to have ended) is in the same format as the beginning date. 
End time is in the same string format as the beginning time. End of the crime period. The crime is usually reported with a period when it took place because sometimes it is difficult to pinpoint the exact time.
Event type is of type string and contains a classifier for the event e.g. VANDALISM. Possible values for said column [4].
Additional event type is a string which is used in conjunction with event type to pinpoint the event type. The field is left empty in case of misdemeanors. Possible values for said column [4].
Type of intrusion describes the method used to commit the unlawful act. Possible values for said column [4].
Security describes how the target of unlawful act was guarded. Possible values for said column [4].
Name of the law based on which the offence was classified.
Paragraph number based on how the offence was classified.
Paragraph text stems from the paragraph number on how the offence was classified.
Section points at specific part of the paragraph.
Point denotes the point number, based on which the offense is classified as. Said field is left blank in the dataset. Can be omitted from the database.
Violation denotes additional legal provision in case of a misdemeanor.
Cost notes how large were the monetary damages. This field consists of a range of integers. The damages are not calculated into exact numbers.
Type of place  denotes the kind of place where the offense took place, it is in a string format. Possible values for said column [4].
County of the offense in in string format.
Municipality of the offence location is in string format.
Crime location denotes settlement unit’s name in string format.
X-coordinate denotes the offense’s X-coordinate in the L-EST coordinate system.
Y-coordinate denotes the offense’s Y-coordinate in the L-EST coordinate system.
Vehicle type is described in string type. Gives a general classification for the vehicle. Possible values for said column [4].
Vehicle model is of string type and specifies the manufacturer of the vehicle.
Vehicle year an integer value which corresponds to the release date for said vehicle.
Type of Crime two character string “KT” or “VT” denoting whether the deed at hand was a  crime and misdemeanor respectively.
Verifying data quality
Due to the nature of unholistic data, depending on the precise scope of the project some of the data can be easily discarded. Whether or not the data has correct values is unknown, but it is believed that since it is filled in by police officers the data itself can not be entirely false. There are possible alternative data sources from the Estonian Open Government Data Portal [2], but said sources do not contain data from  the same time frame (2013-2017).

The data’s quality is lacking in the time department. Which is understandable, if some offense has taken place in a remote location which has not been visited for months e.g. summer house setting a time on such offense might be unreasonable. 

Additional event type column has a lot of information missing, but that is by design. It does not get filled if the event was classified as a misdemeanor in the previous column. Add to that fields that have not been filled because of miscellaneous reasons and said column becomes sparse quickly. Type of intrusion has also been left empty on many occasions. Finally security column is also missing a lot of information.

Vehicle and its related columns are missing information to a great degree and that is understandable. Tying a specific vehicle to a offense without concrete proof is impossible.

Rest of the data does suffer from the occasional missing information but the amount that is missing is negligible and should not affect the project at hand.

3. Project planning 

(Ergo, Anders, Egert)
Business understanding (2,2,2)
Data understanding: determining useful features to use in models, prior data visualisation (3,3,3)
Data preparation: dealing with missing values, dealing with categorical values  (6,6,6)
Modeling: selecting modeling algorithms and training models to prioritize crime according to seriousness,  model for predicting loss of property.  (3,3,3)
Evaluation: evaluating priority model with AUC and loss of property model with accuracy, precision and recall. (2,2,2)
Deployment: visualisation result of models, drawing Estonian map with specific crime frequencies, making poster for poster-session (8,8,8)
