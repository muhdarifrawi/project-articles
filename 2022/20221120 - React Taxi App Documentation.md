# React Taxi App

```
App version: 1.0
App deployment date: 6th November 2022 - 9th November 2022
App development period: 9th November 2022
App article published: 20th November 2022
```

## Content

1. [Introduction](#Introduction)
2. [Walking through the design process](#walking-through-the-design-process)
3. [Issues and limitations](#issues-and-limitations)
   - Plot points for sectors
   - Naming the sectors
   - Finding the number of Taxis within sectors
   - Deployment issues
   - Data point limitations
   - Marker cluster group

## Introduction

This project was planned and designed to showcase my ability in using React JS together with Leaflet and Axios. It was also a project I wanted to use to show to future employers. But after seeing the end product, I don't feel like this is good enough. There were many things that I felt were missing. I will cover more of this in the ["Issues and limitations"](#issues-and-limitations) section of this article. 

## Walking through the design process

### The planning phase

One of the things that I had to decide early was what kind of App this would be. Would be a static webpage or would it be using React JS or would it use Vue JS. Something I learned quite quickly was that you would come across issues if you don't solidify what you would like to use to create your webpage. If you created something in pure HTML/CSS, you would later on find issues to convert them into either React or Vue. Same goes if you were to select either React or Vue. There might be ways you could convert Vue to React or vice versa (not too sure about this, never did look up on it), but converting it back to a static webpage would be a pain. 

Now I can appreciate a little on why planning is really important. If you don't plan for these, you would come across too many problems. 

But let's not pretend. 

I didn't really plan meticulously enough.

I had a few things in mind. I wanted to showcase that I understood how to use Leaflet in Vue. Some of the things you need in Leaflet was some data points too. Without it, there won't be much to show. So I decided that Taxi data would be good. One was because at that time, I wanted to know really how many Taxis were available. The other was that it has 'dynamic' points. The Taxis don't stay at the same spot. According to the API document, the API retrieves the data every 30 seconds[^1]. This would be useful later on when I upgrade the App. I was thinking of doing a 'live' update version of this App.

So other than plotting the Taxi points out, I have always wanted to draw out the various regions of Singapore[^2][^3]. It would be nice to be able to plot it into divisions but I was unable to find a good one in such a short time frame I gave myself. What I managed to find was the Master Plan 2019 Region Boundary[^4]. This proves to be slightly problematic as I began to dig into the data further. All I wanted was to see how it looks. Since there were no demo of it, I simply took in the data to plot it out and afterwards, didn't bother looking for better ones.



## Issues and limitations

## New sources

[Master Plan 2019 Planning Area Boundary-Data.gov.sg](https://data.gov.sg/dataset/master-plan-2019-planning-area-boundary-no-sea)



## Citations

[^1]: [Taxi Availability-Data.gov.sg](https://data.gov.sg/dataset/taxi-availability)
[^2]:[Regions of Singapore - Wikipedia](https://en.wikipedia.org/wiki/Regions_of_Singapore#:~:text=For administrative purposes%2C Singapore is,districts fluctuate with electoral redistricting.)
[^3]:[Singapore: Regions & Major Planning Areas - Population Statistics, Maps, Charts, Weather and Web Information (citypopulation.de)](https://www.citypopulation.de/en/singapore/cities/)
[^4]:[Master Plan 2019 Region Boundary (No Sea)-Data.gov.sg](https://data.gov.sg/dataset/master-plan-2019-region-boundary-no-sea)

