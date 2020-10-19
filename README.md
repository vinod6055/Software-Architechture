# Software-Architechture
The IP_city_weather_condition has the following structure.  
Initial 
Source
IPResponse
servingWebContentApplication
Resources

The above structure contain all the dependency libraries. We have used AWS cloud to deploy this application. Here we have two main functions.
First function makes use of users IP Address to find the location of the user and fetches the weather of that location. 
This function uses  “IPGeolocationAPI” API to request for the weather information from
“Api.openweathermap.org” API.

Code:
if (geolocation.getStatus() == 200) {
                System.out.println(geolocation.getIPAddress());
                System.out.println(geolocation.getCountryName());
                System.out.println(geolocation.getCity());

                String city = geolocation.getCity();

                OkHttpClient client = new OkHttpClient();

                Request request = new Request.Builder()
                        .url("http://api.openweathermap.org/data/2.5/weather?q=" + city + "&APPID=" + WEATHER_API_KEY)
                        .get()
                        .build();
                Response response = null;

                response = client.newCall(request).execute();
                return response.body().string();


 


Second function is fetching weather details by the city.
The user has to type in the name of the place and by using the name of the location “api.openweathermap.org” API fetches the weather information.


public String wheather_by_city(@RequestParam(value = "city", defaultValue = "sydney" ) String city) {
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
                .url("http://api.openweathermap.org/data/2.5/weather?q=" + city + "&APPID=" + WEATHER_API_KEY)
                .get()
                .build();
        Response response = null;
        try {
            response = client.newCall(request).execute();
            return response.body().string();
        } catch (Exception e) {
            e.printStackTrace();
            return "Invalid input :" + e.getMessage();
        }
    }



We have setup a ubuntu instance, installed java and opened port 8080 to run and access the ipwheatherlocation-0.0.1-SNAPSHOT.jar file.
