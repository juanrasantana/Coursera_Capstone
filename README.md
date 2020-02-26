# Final Capstone Project
Final Coursera Capstone for the "IBM Data Science Professional Certificate" course.

# Where to buy a house? A real-state market analysis tool for the city of Santander

## Project description
This project aims at providing useful data for those people that intend to buy a house. Nowadays, buying a house is one of the most important financial decisions that anyone can make in his/her life. Therefore, appropriate tools and information analysis to make a good choice are crucial.

In this project we have focused on the city of Santander, so as to give some insights about the real-state market to future buyers. One of the main problems while buying a house is to distinguish which districts are good, or at least similar to the ones the buyer likes. For example, a buyer might want to buy a house in a particular street, but there are no available houses or they are too expensive. Therefore, the buyer needs to find an alternative area where the services are similar to the original street.

So as to address such issue, this project presents the city of Santander divided in different sections, providing information about the similarities among them using a choropleth map. Therefore, following the results of such map, the buyer can know which are districts that are similar considering the services they provide (hospitals, schools, etc.).

## Project data
So as to perform such analysis and present the results in this project, there are two online datasets available on internet:

[Santander Open Data](http://datos.santander.es/): this is a portal from the municipality of Santander with open data from the city. This portal is implemented using a CKAN platform, which guarantees a standardised data access. Data available in this portal are from heterogeneous sources and cover several domains, including environmental parameters, traffic or urbanism. In our case, we have used part of the urbanism data about the districts in which the city is divided. This dataset is accessible through [the following link](http://datos.santander.es/api/rest/datasets/secciones.csv?items=148&rnd=1880800499) and provides geographical information about the sections in which the city is divided in a CSV format. Data provided includes the sectionId, the district, the population and the polygon defining the Santander sections (in UTM coordinates, so they need to be transformed).

[Foursquare API](https://developer.foursquare.com/): this API provides access to a huge database including geographical information of venues (among other) from all over the world. There is a pricing plan to access this API without limits, however the free limited access provided by foursquare is enough for our case. In this sense, we will make use of one of the regular calls (explore) to which we can make up to 5000 requests per day for free. Additionally, this method provides the possibility of including polygons to delimit the area to explore. The URL endpoint is defined as following:

'https://api.foursquare.com/v2/venues/explore?' + 'client_secret=' + secret_id_fs + '&client_id=' + client_id_fs + '&v=20200201' + '&categoryId=' + categories['hospital'] + '&polygon=' + polygon

The results provided by this API includes all the different elements from the same categoryId found in the specified polygon in a JSON format, including the number of results per request.
