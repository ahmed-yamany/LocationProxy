# LocationProxy

LocationProxy is a Swift utility class for managing location services on iOS devices, providing access to device location, heading, and geocoded placemark information. It is designed for use with iOS 14.0 or later and is intended to simplify location-related tasks in your iOS application.

## Features

- [x] Location service management
- [x] Real-time updates on device heading
- [x] Real-time updates on device location
- [x] Reverse geocoding for location to placemark information
- [x] Handling of location permission requests and user guidance

## Getting Started

To get started with LocationProxy:

1. **Integration**: Add the `LocationProxy.swift` file to your Xcode project. or Add to your project using Swift Package Manager
```
https://github.com/ahmed-yamany/LocationProxy 
```
2. **Initialization**: Use The Shared Instance or Create an instance of `LocationProxy` to manage location services.

   ```swift
   let locationProxy = LocationProxy.shared
   ```

 ##
1. Enable Location Services: To start receiving location and heading updates, use the enable method.
   
    ```swift
    locationProxy.enable()
    ```
2. Disable Location Services: To stop location and heading updates, use the disable method.
   ```swift
    locationProxy.disable()
   ```
3. Accessing Location and Heading Updates: Subscribe to the heading and locations publishers to receive updates. For example:
   ```swift
     let locationsSubscriber = locationProxy.locations
           .sink { completion in
                switch completion {
                case .finished:
                    break
                case .failure(let error):
                    print(error.localizedDescription)
                }
            } receiveValue: { locations in
                print(locations.first?.coordinate.latitude)
                print(locations.first?.coordinate.longitude)
            }
     let locationsCancelable = AnyCancellable(locationsSubscriber)
   ```
4. Accessing Geocoded Placemarks:
   ```swift
      let placemarkSubscriber = locationProxy.placemarks
            .sink { completion in
                switch completion {
                case .finished:
                    break
                case .failure(let error):
                    print(error.localizedDescription)
                }
            } receiveValue: { placemarks in
                print(placemarks.first?.country)
                print(placemarks.first?.locality)
                print(placemarks.first?.administrativeArea)
                print(placemarks.first?.postalCode)
            }
        let placemarkCancelable = AnyCancellable(placemarkSubscriber)
   ```
5. Handling Location Access Denied:

    If the user denies location access, a user-friendly alert will be displayed. This alert provides an option to open the device settings for adjusting permissions.

## Requirements
    iOS 14.0 or later
    Swift 5.0 or later
## Author
   [Ahmed Yamany](https://www.linkedin.com/in/ahmed-yamany/) 
