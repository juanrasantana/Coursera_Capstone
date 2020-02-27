# Final Capstone Project
Final Coursera Capstone for the "IBM Data Science Professional Certificate" course. This project has been developed using a IBM jupyter notebook and can be accessed [through this link](https://eu-gb.dataplatform.cloud.ibm.com/analytics/notebooks/v2/be003d54-c652-4600-88ba-771bf128ef02/view?access_token=3a781152ef1bd241d3c0d99c3a2b3598db3cd864b07d9dd19adc7cfc82364e81).

# Where to buy a house? A real-state market analysis tool for the city of Santander

## Project description
This project aims at providing useful data for those people that intend to buy a house. Nowadays, buying a house is one of the most important financial decisions that anyone can make in his/her life. Therefore, appropriate tools and information analysis to make a good choice are crucial.

In this project we have focused on the city of Santander, so as to give some insights about the real-state market to future buyers. One of the main problems while buying a house is to distinguish which districts are good, or at least similar to the ones the buyer likes. For example, a buyer might want to buy a house in a particular street, but there are no available houses or they are too expensive. Therefore, the buyer needs to find an alternative area where the services are similar to the original street.

So as to address such issue, this project presents the city of Santander divided in different sections, providing information about the similarities among them using a choropleth map. Therefore, following the results of such map, the buyer can know which are districts that are similar considering the services they provide (hospitals, schools, etc.).

![alt text](https://github.com/juanrasantana/Coursera_Capstone/raw/master/santander_city_sections.png "Santander city divided in sections")

## Project data
So as to perform such analysis and present the results in this project, there are two online datasets available on internet:

[Santander Open Data](http://datos.santander.es/): this is a portal from the municipality of Santander with open data from the city. This portal is implemented using a CKAN platform, which guarantees a standardised data access. Data available in this portal are from heterogeneous sources and cover several domains, including environmental parameters, traffic or urbanism. In our case, we have used part of the urbanism data about the districts in which the city is divided. This dataset is accessible through [the following link](http://datos.santander.es/api/rest/datasets/secciones.csv?items=148&rnd=1880800499) and provides geographical information about the sections in which the city is divided in a CSV format. Data provided includes the sectionId, the district, the population and the polygon defining the Santander sections (in UTM coordinates, so they need to be transformed).

[Foursquare API](https://developer.foursquare.com/): this API provides access to a huge database including geographical information of venues (among other) from all over the world. There is a pricing plan to access this API without limits, however the free limited access provided by foursquare is enough for our case. In this sense, we will make use of one of the regular calls (explore) to which we can make up to 5000 requests per day for free. Additionally, this method provides the possibility of including polygons to delimit the area to explore. The URL endpoint is defined as following:

'https://api.foursquare.com/v2/venues/explore?' + 'client_secret=' + secret_id_fs + '&client_id=' + client_id_fs + '&v=20200201' + '&categoryId=' + categories['hospital'] + '&polygon=' + polygon

The results provided by this API includes all the different elements from the same categoryId found in the specified polygon in a JSON format, including the number of results per request.
Using both sources of information we will be able to provide a choropleth map showing the sections of the city which are similar. On the one hand, the urbanism data from the open data platform will provide the means to draw the maps and make the appropriate requests to the foursquare API. On the other hand, the foursquare API will provide the different existing services per section in the city. Using this information along with non-supervised algorithms such as K-means, we can divide the city in sections showing similarities for the real-state buyers.

## Methodology followed
So as to obtain the similar sections in the city of Santander, we have followed a well-defined methodology, described following the steps below:
1.	Obtain the geographical data from Santander (polygons in which the city is divided) and create the dataframe. This data is obtained from the Santander Open Data portal using a REST service.
2.	Format the data into a usable dataframe. The main issue here is to transform the UTM coordinates to Latitude and Longitude used by the Foursquare API.
3.	Draw the map depending on the inhabitants in each district. To this end, we have used the folium library for python.
4.	Get information from foursquare about each district: hospitals, schools, etc. Additionally, data obtained is processed to extract the required parameters (e.g. number of venues per section).
5.	Normalise the information obtained from Foursquare to be used with machine learning techniques.
6.	Use a non-supervised algorithm to divide the districts depending on their similarity.
7.	Finally, draw a map using folium to show similarities among the different sections of the city.

## Results
As we can see in the results, there are different areas of the city that are quite similar among them. Even if some of them are in the city centre and in the suburbs. At least regarding to the services provided.

![alt text](https://github.com/juanrasantana/Coursera_Capstone/raw/master/santander_city_sections_similarity.png "Choropleth map of Santander city sections showing their similarity")

For example, it is clear that some parts of the city center (soft green, between the orange and green) provides similar services to other parts of the city which are further, while the prices are much higher. Therefore, although the advantages of living in the city centre could not be represented clearly in this map, the cost of the houses can be worth the money. On the other hand, it is clear that the area where the beaches are located, are represented in one single cluster (orange), even if we did not consider beaches as data input.

## Conclusions and next steps
As we saw in the report, this method allows us to obtain useful information at the time of buying a house in the city of Santander. However, this report can be enlarge using more information sources, such as more types of venues (now we are limited by foursquare free plan). 
Finally, it would be great to perform a long-term data gathering from real-state webpages to obtain a large dataset of house prices in the different sections of the city. This will allow us to understand the impact on the house prices the different services can have. Of course, enlarge this project to other cities could give us a wider knowledge of the real-state market in a country.
