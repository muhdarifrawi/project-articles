# React Taxi App

```
App version: 1.0
App deployment date: 6th November 2022 - 9th November 2022
App development period: 9th November 2022
App article published: 20th November 2022
```

## Content

1. [Introduction](#Introduction)
2. [Walking through my thought process](#walking-through-my-thought-process)
3. [Issues and limitations](#issues-and-limitations)
   - Data point limitations
   - Plot points for sectors
   - Naming the sectors
   - Passing `props` 
   - Marker cluster group
   - Finding the number of Taxis within sectors
   - Deployment issues
   - Showing the number of available Taxis

## Introduction

This project was planned and designed to showcase my ability in using React JS together with Leaflet and Axios. It was also a project I wanted to use to show to future employers. But after seeing the end product, I don't feel like this is good enough. There were many things that I felt were missing. I will cover more of this in the ["Issues and limitations"](#issues-and-limitations) section of this article. 

## Walking through my thought process

One of the things that I had to decide early was what kind of App this would be. Would it be a static webpage or would it be using React JS, or would it use Vue JS. Something I learned quite quickly was that you would come across issues if you don't solidify what you would like to use to create your webpage. If you created something in pure HTML/CSS, you would later on find issues to convert them into either React or Vue. Same goes if you were to select either React or Vue. There might be ways you could convert Vue to React or vice versa (not too sure about this, never did look up on it), but converting it back to a static webpage would be a pain. 

Now I can appreciate a little on why planning is really important. If you don't plan for these, you would come across too many problems. 

But let's not pretend. 

I didn't really plan meticulously enough.

I had a few things in mind. I wanted to showcase that I understood how to use Leaflet in React. Some of the things you need in Leaflet was some data points too. Without it, there won't be much to show. So I decided that Taxi data would be good. One was because at that time, I wanted to know really how many Taxis were available. The other was that it has 'dynamic' points. The Taxis don't stay at the same spot. According to the API document, the API retrieves the data every 30 seconds[^1]. This would be useful for the later stage when I upgrade the App. I was thinking of doing a 'live' update version of this App.

So other than plotting the Taxi points out, I have always wanted to draw out the various regions of Singapore[^2][^3]. It would be nice to be able to plot it into divisions but I was unable to find a good one in such a short time frame I gave myself. What I managed to find was the Master Plan 2019 Region Boundary[^4]. This proves to be slightly problematic as I began to dig into the data further. All I wanted was to see how it looks. Since there were no demo of it, I simply took in the data to plot it out and afterwards, didn't bother looking for better ones. So at the end, I ended up using the plotlines that I dug up from that data. Though I would want to look for better ones.

Putting them together was no easy feat. My focus was to create only using Reacts' function components. I had used the class based components before. But from what I heard, React would be shifting more into function based components[^5]. I had to read up a little to understand how I should go about only using functional components. Initially I had issues with how I should go about passing data over. I knew I had to use `props` but I didn't know how to properly do so. I was too engrossed on getting the plotlines that I overlooked on how the data architecture should look like. So at one point I had to pause awhile and ponder how I should be passing `props` over. What I ended with was `GeoData` &rarr; `Taxi` &rarr; `Map`.

Perhaps I could have done better. But this was the best I could do for now. 

I had some minor issues with getting the icons to appear nicely. There was the issue of doing markercluster as well. I also didn't know how I should go about designing the page as well. So I ended up with a too simplistic design. But I managed to show what I needed within the webpage.

## Issues and limitations

### Data Point Limitations

As stated earlier, I wanted to quickly find a dataset that I could quickly use to create polylines for Leaflet. There was no demo for the GeoJSON[^4] I found so I had to plot it out to see how it would look. But little did I know that it would take me some time to plot it out. And by the time I was done plotting it out, I didn't want to waste more time to plot new ones. 

If you looked into the GeoJSON, you'll see that in order for me to use this as a polyline for Leaflet, I would have to clean it up a little. I had to dive right in to each coordinates and pick out the Latitude and Longitude. I would also have to divide them up into sectors. Now these sectors are unlabeled too. So I needed to name them as well. 

To resolve the coordinates issue, I ran this code:

```JavaScript
const getCoordinates = (data) => {
        let compiledCoordinates = []
        for(let i=0; i < data.features.length; i++){
            let level1 = data.features[i]
            for(let j=0; j < level1["geometry"]["coordinates"].length; j++){
                let level2 = level1["geometry"]["coordinates"][j][0]
                let cleanCoordinate = level2.map(i => i.slice(0,-1).reverse())
                compiledCoordinates.push(cleanCoordinate)
            }
        }
        setCoordinates(compiledCoordinates);
    }
```

This would take only the first two indexes and reverse them to correct the Latitude Longitude (LatLong) issue. After which, this newly created array would be pushed into a new array for the polyline. The array for the polyline would have grouped arrays consisting of many LatLong arrays, where each group would represent one region. 

As for naming each region, after plotting the raw LatLong that I had, I manually looked at what each plotted region represented and created an array of names for it. I placed it into a function so that it would be easier for me to render out the name into Leaflet's layer control.

```javascript
function mapArea(index) {
        let mapAreaArr = [
            "Pulau Satumu (dock)",
            "Pulau Satumu",
            "Island Southeast of Pulau Senang",
            "Pulau Senang",
            "Sea Area, East of Pulau Pawai",
            "Sea Area, North of Pulau Pawai",
            "Pulau Pawai",
            "Sea Area, West of Pulau Semakau",
            "Pulau Sebarok",
            "Pulau Sudong",
            "Pulau Jong",
            "Pulau Salu",
            "Pulau Semakau",
            "Pulau Hantu Kecil",
            "Pulau Hantu Besar",
            "Pulau Busing",
            "West of Sultan Shoal",
            "Sultan Shoal",
            "Pulau Bukom",
            "Pulau Pergam",
            "West of Singapore",
            "Pulau Sarimbun",
            "Pulau Seletar",
            "North of Singapore",
            "Pulau Ketam",
            "Pulau Ubin",
            "North-East of Singapore",
            "Sea Area, North-East of Pulau Tekong",
            "Pulau Tekong",
            "Sea Area, South-East of Singapore",
            "Sea Area, East of Singapore",
            "East of Singapore",
            "Pulau Subar Laut (Breakwater)",
            "Pulau Subar Laut",
            "Pulau Subar Darat",
            "South of Pulau Kusu (Breakwater)",
            "Pulau Kusu",
            "North of Pulau Kusu (Breakwater)",
            "St. John's Island, Lazarus Island, Pulau Renget",
            "Pulau Tekukor",
            "South of Sentosa (Breakwater)",
            "Sea Area, South-East of Sentosa",
            "Southernmost Point of Continental Asia",
            "Island, South-West of Sentosa",
            "South-West of Sentosa (Breakwater)",
            "South-West of Sentosa (Breakwater)",
            "South-West of Sentosa (Breakwater)",
            "Sea Area, North of Sentosa",
            "South of Singapore"
        ]

        return mapAreaArr[index]
    }
```

## New sources

[Master Plan 2019 Planning Area Boundary-Data.gov.sg](https://data.gov.sg/dataset/master-plan-2019-planning-area-boundary-no-sea)



## Citations

[^1]: [Taxi Availability-Data.gov.sg](https://data.gov.sg/dataset/taxi-availability)
[^2]:[Regions of Singapore - Wikipedia](https://en.wikipedia.org/wiki/Regions_of_Singapore)
[^3]:[Singapore: Regions & Major Planning Areas - Population Statistics, Maps, Charts, Weather and Web Information (citypopulation.de)](https://www.citypopulation.de/en/singapore/cities/)
[^4]:[Master Plan 2019 Region Boundary (No Sea)-Data.gov.sg](https://data.gov.sg/dataset/master-plan-2019-region-boundary-no-sea)

[^5]:[Do I need to rewrite all my class components?](https://reactjs.org/docs/hooks-faq.html#do-i-need-to-rewrite-all-my-class-components)
