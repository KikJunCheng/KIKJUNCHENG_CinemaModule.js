# Assignment 1



<!-- You will only need one file, ie, your node module, for this assignment.

In this readme file, describe how to use your node module. It could be similar to **app.js** from Lab2, where you call some functions in your node module and display the output. Describe how to setup your node module, if any. Describe how to call the functions, what parameters required and so on.

You can press **Ctrl+Shift+V** in this file in Visual Studio Code to see a live preview of the readme file.

For some tips in formatting text in readme file, refer to https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax -->

<!-- Data Structure -->
<h1>First Function</h1>
The first function I implemented is called `viewAllAvailableSeats`. This function accepts four parameters: cinema, movie, date and time all in 'String'.

First, the function searches through the `showtime` array to identify the showtime object that matches the cinema and movie entered by the user. Once the matching showtime object is found, the function then searches through its screenings to identify the screening that matches the date and time provided by the user.

Next, based on the selected screening, the function loops through its seats array to check the status of each seat. If a seat's status is marked as "Vacant", that seat will be added to a separate array called `vacantSeats`.

Finally, the function returns the `vacantSeats` array and displays the available seats so that the user can see which seats are currently available for booking.

<h1>Second Function</h1>
The second function I implemented is called `bookOneOrManyTicket`. This function accepts 8 parameters: `cinema`, `movie`, `date` and `time` as strings, `pax` as an integer, `age` as an array of integers, and `occupation` and `seatNos` as arrays of strings.

The function first searches the `showtime` array for a matching cinema and movie based on the user's input. Then, within the matching showtime object, it searches for the screening that matches the selected date and time. After that, it retrieves the seats in the selected screening with `status == "vacant"`. It also validates that the number of selected seats matches the number of people booking.

The function then checks whether `pax` is an integer and is greater than 0. It must also be equal to the length of the `seatNos` array provided by the user, or else it will return an error message. After that, it checks whether the seats selected by the user are occupied or not. If any selected seat is occupied, it will return an error message.

Then, the function checks whether the screening time selected by the user is during peak hours or not. If it is, the function will use the peak-hour price. The ticket price calculation will also check whether each person is an adult or a child. If the person is an adult, they will be charged the adult price. If the person is a child, they will be charged the child price. It will then check whether the person is a student. If the person is a student, they will get the student price.

Finally, the function saves the tickets to the `myBookings` array as JSON objects, and each selected seat is marked as occupied.
<!-- Third Function -->
<h1>Third Function </h1>
The third function I implemented is called `findBestNearestCinema`. This function accepts 3 parameters: latitude and longitude as floats, and movie as a string.

It will first match the cinemas based on the movie the user wants to watch. Then, based on the latitude and longitude provided by the user, together with the latitude and longitude of the cinema location hardcoded in the system, it calculates the direct distance between the cinema and the user's location using the Haversine formula. The Haversine formula can calculate the angular distance, unlike Pythagoras, which only calculates flat distance. Since the Earth is round, I use the Haversine formula instead.

I first convert all the latitude and longitude values to radians. Then, I find the difference in latitude between the user's location and the cinema location, as well as the difference in longitude between the user's location and the cinema location.

After using the Haversine formula to find the angular distance between the user's location and the cinema, I multiply the angular distance by the Earth's radius, `6371`, to find the distance between the user's location and the cinema location in kilometres.

I set the variable `shortestDistance` to infinity initially, so whenever a shorter distance is found, it will update the `shortestDistance` variable. Based on the distance, it will create a `nearestCinema` JSON object to store the cinema name, movie name and distance whenever the shortest distance is found.

Finally, it prints the recommended cinema and the distance in kilometres for the user.
<!-- Fourth Function -->
<h1>Fourth Function</h1>
The fourth function I implemented is called `findBestSeats`. Its purpose is to recommend consecutive seats for a group of people who want to sit together. It accepts 5 parameters, movie, cinema, date, time in string and pax in integer. 

First, the function identifies the screening selected by the user and calls the first function, `viewAllAvailableSeats()`, to retrieve all the vacant seats. These vacant seats are then stored in an array called `vacantSeats`.

Next, the function validates the number of passengers provided through the `pax` parameter. If the number of passengers is less than or equal to zero, or if it is not an integer, the function will stop and display an error message.

If the validation passes, the function uses two nested loops to find consecutive seats. The outer loop goes through the vacant seats and selects a possible starting seat. For example, if there are 5 vacant seats and the user requests 4 seats, the outer loop will run with `i` equal to 0 and 1. This is because we subtract the number of passengers from the total number of vacant seats, giving us 1. Therefore, there are only 2 possible starting positions where a group of 4 seats could fit.

For each starting seat, the inner loop checks the following seats. It starts with `j` equal to 1 because the first seat has already been selected by the outer loop. For example, if `i` is 0 and `j` is 1, the function accesses `vacantSeats[1]`, which represents the next seat after the starting seat.

To determine whether the seats are consecutive, I use `parseInt()` together with `substring(1)` to extract only the numeric portion of the seat number, excluding the row letter. For example, A1 becomes 1 and A2 becomes 2. The function then checks whether the next seat number is equal to the current seat number plus `j`.

If the condition is not met, it means the seats are not consecutive, so the inner loop will break and the outer loop will move on to the next possible starting seat. However, if the condition is met, the next seat will be added to a temporary array called `selectedSeats`.

Once the inner loop finishes, the function checks whether the length of `selectedSeats` is equal to `pax`. If both values are equal, it means enough consecutive seats have been found. The temporary array will then be assigned to `bestSeats`, and the outer loop will break because a suitable recommendation has been found.

Finally, the function checks whether the length of `bestSeats` matches the number of passengers. If it does, the recommended seats will be displayed. Otherwise, the function will display a message saying that there is no suitable seat recommendation.

<!-- Fifth Function -->
<h1>Fifth Function</h1>
The fifth function I implemented is called `feedback`. Its purpose is to allow users to rate the cinema they have visited before. It accepts 3 parameters: `cinema` as a string, `rating` as an integer and `reviews` as a string.

It first finds the cinema the user wants to review by looping through the `showtime` array to find the cinema that matches the `cinema` string provided by the user. If it cannot find the cinema, it will return an error message.

Then, it checks whether the rating provided by the user is an integer and whether it is within the range of 1 to 5. If it does not meet the conditions, it will return an error message.

After that, it saves the user's information to `UserReviews` in the showtime object. It will then store all the ratings given by users in a variable called `totalRating` and update the cinema's rating by dividing the total rating by the number of review records to calculate the average rating.

Finally, it will print the ratings given by users and the reasons behind them using a `for` loop.

For this function you can use an array to store multiple ratings and reasons then using a for loop to call this function multiple times.

<!-- Sixth Function -->
<h1>Sixth Function</h1>
The sixth function I implemented is called `findBestCinema`. It only accepts one parameter, `movie`, as a string.

It first finds the cinemas that are showing the movie the user wants to watch by using a `for` loop to go through the `showtime` array and an `if` condition to match the `movie` parameter with the movie string in `showtime`. It then stores the cinemas in the `cinemaSelected` array.

After that, a `for` loop is used to go through `cinemaSelected`, and a `currentRating` variable is set to -100 initially. Whenever it is lower than a cinema's rating, it will update itself to the higher rating.

Thus, it will display the cinemas from the highest-rated to the lowest-rated.

<!-- Seventh Function -->
The seventh function I implemented is called `cancelBooking()`. It accepts one parameter, `bookingID`, which is used to identify the booking the user wants to cancel.

It first gets the current date and time using `new Date()`. Then, it uses a `for` loop to go through the `myBookings` array to find the booking that matches the `bookingID` provided by the user.

Once it finds the matching booking, it retrieves the movie date and time from the booking record. It then uses the `split()` method to separate the date and time into individual parts so that they can be used to create a new `Date` object representing the movie screening date and time.

After that, it subtracts the current date and time from the movie screening date and time to calculate the time difference in milliseconds. It then converts the time difference from milliseconds to hours by dividing it by `1000 * 60 * 60`.

The function then checks whether the remaining time before the movie screening is less than 8 hours. If it is, the booking cannot be cancelled, and it will display an error message. Otherwise, it deletes the booking from the `myBookings` array and displays a successful cancellation message.

Finally, it prints the updated `myBookings` array.
<!-- How to call function -->
# References
<!-- Provide the references that you have used to support your assignment.  -->
https://www.gv.com.sg/
1. I used AI to find out how do i convert lattitude and longitude into distance in kilometers using the Haversine formula
2. I used AI to explore creative ways to recommend seats to users, such as finding consecutive seats by checking whether the next seat number is equal to the current seat number plus 1.
3. I used AI to understand the syntax for converting a string into a Date object in JavaScript.
