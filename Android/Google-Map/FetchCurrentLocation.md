
The Google Maps Fused Location Provider API is part of the Google Play Services Location API. It provides an efficient way to retrieve the user’s current location with low power usage by intelligently combining location data from various sources such as:

GPS: High accuracy, but uses more battery.
Wi-Fi: Good for indoor locations and faster retrieval of the location.
Cellular Towers: Used when GPS or Wi-Fi is unavailable.
Bluetooth: Can be used for proximity-based location.
Key Features:
Location Accuracy: It balances power consumption with the required accuracy level (e.g., high-accuracy for GPS or low-power for coarse location).
Location Updates: It supports periodic location updates with a defined interval.
Geofencing: It allows defining geographic boundaries to trigger actions when the user enters or exits those regions.
Activity Recognition: It can also detect the user’s movement (e.g., walking, running, driving).
Power Efficiency: Combines multiple location providers to reduce battery consumption.

Implementations
Created a Location data class with two parameters, longitude and latitude, and a function which returns the LatLng object.
In the app module, we have defined one provide function that returns FusedLocationProviderClient using LocationServices that invoke the getLocationProviderClient() function.
We have followed the Repository pattern, where I had defined IRepossitory, in IRepository I have defined all the methods such as getCurrentLocation(), checkLocationPermission(), isGpsEnable(), observeLocationUpdates()
In the Repository class, it has context and a FusedLocationProviredClient object. I have implemented the logic of these functions. The getCurrentLocation() method returns the Result of Location object, it first check the runtime permission is granted or not using checkSelfPermisson() method, if the permission is granted then get the location using fusedLocationClient.getCurrentLocation(). And we also implemented isGpsEnable() method using the LocationManager.isProvidedEnable() function. We also implemented observeLocationUpdate() function, where we have invoked the fusedLocationClient.requestLocationUpdates() function which takes locationCallback and locationRequest.
Then I implemented the ViewModel by defining the MutableStateFlow and StateFlow and implemented the methods of the Repository.
And then I created the UI using compose.
