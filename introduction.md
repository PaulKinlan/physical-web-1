##The Big Idea
The Physical Web extends the same web we know and love into the physical world around us. This involves creating an open ecosystem where devices can broadcast a URL to any nearby smart display (phone, tablet, glasses, etc) can then see these URLs and offer them up to the user. It mirrors the basic behavior we have today with a search engine:

* The user asks to see what's nearby (widget, notifications bar, etc)
* A ranked list of URLs is shown
* The user picks one
* The URL is opened in a full screen browser window.

Even though this is a fairly simple idea, it immediately generates lots of questions so let's get them out of the way:

##1. What's wrong with native apps?
Nothing! Native apps are great but they're just not mathematically practical. If we believe in Moore's Law at all, there will be 1000s of these smart devices very soon and the native app approach breaks down. Are you really going to download an app when you pass a vending machine? Yahoo used to be a fixed hierarchy of links and  just give it up once the web exploded. The same thing will happen with smart hardware and apps.


##2. Sounds like you'll be pestering people with notifications
A core principle of this system is **no proactive notifications**. The user will only see a list of nearby devices when they ask. If things were to buzz, it would generate immediate frustration. Push notifications, in general are too easily abused.

##3. Isn't there going to be a big list to choose from?
At first, the nearby smart devices will be small but if we're successful, there will be many to choose from and that does raise an important UX issue. This is where ranking comes in. Today, we are perfectly happy typing "tennis" into a search engine and getting millions of results back, we trust that the first 10 are the best ones. The same applies here. The phone app can sort by both signal strength (more on that below) as well as personal preference (you've used this one before). Clearly there is lots of work to be done here, we don't want to minimize this task but we feel that ranking can get us very far for the first few versions of this project.

##4. Is this secure?
This first version is broadcasting URLs in the clear, there is no encryption so in it's current form, it's not yet secure. That is why we're initially suggesting this to be used in public spaces. However, that being said, there are many ways you could imaging making a URL secure, e.g. a rotating token that requires a login/cookie to decode. One of the huge values of URLs is that they are so flexible and encourage this further evolution.

##5. What about SPAM?
With any open system, there will be people that try to exploit it. There will likely be many solutions around this problem but again, we can start with the web. Search engines today have this issue and are fairly effective and displaying the correct web sites in your search results. That same approach would apply here. Combine that with historical results of who clicks on what and it's possible to build a fairly robust ranking model and only show the proper devices. However, there is likely much more we can do here and we hope to encourage other ideas on how to solve this problem in a more robust way.

##6. Why URLs?
We could have gone with a central server and used generated IDs. However, the value of a URL is that it is a known part of the web, very flexible, and most importantly, decentralized. URLs allow anyone to play and no central server to be the bottleneck. This is one of the core principles of the web and critical to keep alive.

That being said, we completely expect others to do just that: build a url+ID model that goes through a central server. That is perfectly acceptible and to be encouarged. Systems like that are likely to provide much better security and vetting of sites. But that is the beauty of URLs, there can be as many of these as you'd like and the system still works seamlessly.  

##7. Which platforms will you support?
This is meant to be an extension of the web so it should work on every platform. We expect that each will experiment with a different UX to show the nearby devices. For example, Android might use a widget or even integrate with Google Now. iOS could use their notification manager (silently!) or even just have an app that you can open. We hope to see lots of experimentation here on how various platforms choose to show and rank this information.

At this point, we have an android application and an AppEngine Server app that is open sourse. We hope this will be used and ported to other platforms.

##8. Can't the user be tracked?
Our current URL broadcast method involves no interaction between that device and the user's phone. They can just receive the URLs much like they can see nearby wifi hotspots. This means a user can't be tracked simply by walking past a broadcasting device. This was very much by design to keep users silent passage untrackable. However, once the user does click on a URL, they are then known to that website. 

The search agent on the phone may keep track of which devices the user taps on so they can improve the ranking in the future. Of course, this too needs to be discussed and the possibly offered to the user as an option so they are in control of how this information is stored.

##Next
The next document to read would be the technical [overview](http://github.com/scottjenson/physical-web/blob/master/technical_overview.md) document