# Tumblr offline
## November 19, 2013


### (Much of this is outdated)

---

# Key values

* Big emphasis on having the app be as functional as possible without a connection
* Really not doing anything too clever here

---

# Navigation

* Never prevent the user from navigating just because they’re offline
* Very few “are we online?” checks in general
* An alert is shown when the app is foregrounded if there’s no connection
* Screens will just be empty if the data isn’t already cached

---

# Displaying API data

* Core Data basically just used as a cache
    * When most recent data is fetched from can API route, delete all older data for that route
    * Perform general cleanup when application terminates
* If offline when user makes a new request, just call the controller back immediately without any new data

---

# Images

* `TMCache` (open source)
    * Hybrid disk/memory cache (only using the disk part currently)
* Trim to max size on application background
    * Could keep it below limit but wanted to save CPU

---

# POST requests

* `OutstandingRequest` Core Data entity
    * URL/parameters
    * Retry count/created date
* Provide immediate UI feedback
* Retry whenever the application is foregrounded
* Error reporting/confirmation is currently lacking

---

# `TMRequestProxy`

* Delegate of an `NSOperation` subclass representing the actual HTTP request
    * Handles deleting the persistent object when the request completes or exceeds retries/max. age
* Can notify UI regarding upload progress
* This all happens regardless of if the user is online or offline

---

# Push notifications

* Can’t unregister from APNS directly
    * Use your own server
    * Use Apple’s feedback mechanism to catch uninstalls
* Database wiped when user logs out
    * Logging out while offline = still receive push notifications
    * Persist registered/unregistered state separately, sync up with the server once back online