Download Link: https://assignmentchef.com/product/solved-cs2030s-lab-4-snatch
<br>
Snatch is yet another transport service provider trying to vie for a place in the public transport arena.

Snatch provides three types of ride services:

JustRideFare is based on the distance @ 22 cents per kmFare is the same regardless of the number of passengers (pax)There is no booking fee.A surcharge of 500 cents if a ride request is issued between the peak hour of 600 hrs to 900 hrs, both inclusiveTakeACabFare is based on the distance @ 33 cents per km, but there is a booking fee of 200 centsFare is the same regardless of the number of passengers (pax)No peak hour surchargeShareARideFare is based on the distance @ 50 cents per kmFare is divided equally among the number of passengersThere is no booking fee.Any fractional part of the fare is absorbed by your friendly driverA surcharge of 500 cents if a ride request is issued between 600 hrs to 900 hrs, both inclusiveIn addition, there are two types of drivers under Snatch. Each can provide a subset of the services above.

NormalCab drivers provide JustRide and TakeACab services.PrivateCar drivers provide JustRide and ShareARide services.A customer can issue a Snatch ride request, specified by the distance of the ride, the number of passengers, and the time of the request.

TaskYou shall be given a request, followed by a list of NormalCab or PrivateCar drivers together with their corresponding waiting times. A booking is a pairing of a driver with the request. The task is to find the best booking with the lowest fare by matching the available drivers based on the services they provide to the given request. Break ties among the same lowest fares by selecting the booking with the smaller waiting time.

You may assume that no two bookings have the same fare and the same waiting time.

This task is divided into several levels. Read through all the levels to see how the different levels are related.

Remember to:

always compile your program files first before using jshell to test your programuse checkstyle and javadoc comments to enhance code readability and facilitating code review

Level 1Define a Request class to handle a request comprising the distance, number of passengers, and time.

$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test1.jshjshell&gt; new Request(20, 3, 1000)$.. ==&gt; 20km for 3pax @ 1000hrsjshell&gt; new Request(10, 1, 900)$.. ==&gt; 10km for 1pax @ 900hrsjshell&gt; /exit

Level 2Now include the JustRide and TakeACab services. Note that every service needs to implement the computeFare method that returns the fare in cents.

$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test2.jshjshell&gt; new JustRide()$.. ==&gt; JustRidejshell&gt; new JustRide().computeFare(new Request(20, 3, 1000))$.. ==&gt; 440jshell&gt; new JustRide().computeFare(new Request(10, 1, 900))$.. ==&gt; 720jshell&gt; new TakeACab()$.. ==&gt; TakeACabjshell&gt; new TakeACab().computeFare(new Request(20, 3, 1000))$.. ==&gt; 860jshell&gt; new TakeACab().computeFare(new Request(10, 1, 900))$.. ==&gt; 530jshell&gt; /exit

Level 3Now, include a NormalCab driver who is identified by its license plate number (a string) and the passenger waiting time in minutes.

Then, add a Booking class that takes in a driver and a request. From the services that a driver provides, the best service with the lowest fare is selected.

Two bookings may be compared using their computed fares; if both fares are the same, prefer the one with the shorter waiting time.

$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test3.jshjshell&gt; new NormalCab(“SHA1234”, 5)$.. ==&gt; SHA1234 (5 mins away) NormalCabjshell&gt; new Booking(new NormalCab(“SHA1234”, 5), new Request(20, 3, 1000))$.. ==&gt; $4.40 using SHA1234 (5 mins away) NormalCab (JustRide)jshell&gt; new NormalCab(“SHA2345”, 10)$.. ==&gt; SHA2345 (10 mins away) NormalCabjshell&gt; new Booking(new NormalCab(“SHA2345”, 10), new Request(10, 1, 900))$.. ==&gt; $5.30 using SHA2345 (10 mins away) NormalCab (TakeACab)jshell&gt; Booking b1 = new Booking(new NormalCab(“SHA2345”, 10), new Request(10, 1, 900))jshell&gt; Booking b2 = new Booking(new NormalCab(“SHA2345”, 10), new Request(10, 1, 900))jshell&gt; b1.compareTo(b2) == 0$.. ==&gt; truejshell&gt; Booking b3 = new Booking(new NormalCab(“SHA1234”, 5), new Request(10, 1, 900))jshell&gt; Booking b4 = new Booking(new NormalCab(“SHA2345”, 10), new Request(10, 1, 900))jshell&gt; b3.compareTo(b4) &lt; 0$.. ==&gt; truejshell&gt; /exit

Level 4Now include the ShareARide service and PrivateCar driver.

You should aim to make the Booking class general such that it does not need to check for any invalid pairing, say between PrivateCar driver and TakeACab service. If you have designed your program appropriately, then extending your program with additional drivers and services would not require any modification to existing classes.

$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test4.jshjshell&gt; new ShareARide()$.. ==&gt; ShareARidejshell&gt; new PrivateCar(“SMA7890”, 5)$.. ==&gt; SMA7890 (5 mins away) PrivateCarjshell&gt; new Booking(new PrivateCar(“SMA7890”, 5), new Request(20, 3, 1000))$.. ==&gt; $3.33 using SMA7890 (5 mins away) PrivateCar (ShareARide)jshell&gt; new PrivateCar(“SLA5678”, 10)$.. ==&gt; SLA5678 (10 mins away) PrivateCarjshell&gt; new Booking(new PrivateCar(“SLA5678”, 10), new Request(10, 1, 900))$.. ==&gt; $7.20 using SLA5678 (10 mins away) PrivateCar (JustRide)jshell&gt; Booking b1 = new Booking(new PrivateCar(“SMA7890”, 5), new Request(10, 1, 900))jshell&gt; Booking b2 = new Booking(new PrivateCar(“SLA5678”, 10), new Request(10, 1, 900))jshell&gt; b1.compareTo(b2) &lt; 0$.. ==&gt; truejshell&gt; /exit

Level 5Now complete the task by defining the findBestBooking method to return the best booking given a request, and an array of drivers with their waiting times. Save the method in the file level5.jsh.

Assume that no two bookings have the same fare and the same waiting time.

$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order level5.jsh &lt; test5.jshjshell&gt; findBestBooking(new Request(20, 3, 1000),…&gt; new Driver[]{new NormalCab(“SHA1234”, 5), new PrivateCar(“SMA7890”, 10)})$.. ==&gt; $3.33 using SMA7890 (10 mins away) PrivateCar (ShareARide)jshell&gt; findBestBooking(new Request(10, 1, 900),…&gt; new Driver[]{new NormalCab(“SHA1234”, 5), new PrivateCar(“SMA7890”, 10)})$.. ==&gt; $5.30 using SHA1234 (5 mins away) NormalCab (TakeACab)jshell&gt; /exit