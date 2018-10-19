+++
title = "Using XPlot for rugby league visualisations"
description = ""
date = 2017-05-10
slug = "using-xplot-for-rugby-league-visualisations"
+++

I want an easy way to visualise rugby league match data for the team I support.

It's been a couple of years since I last played around with F# so I'm going to use XPlot which will also give me the chance to look into the impressive ionide and paket. I'm going to start with a scatter chart showing the times tries were conceded each match - I'll continue to add more visualisations as the season progresses.

## The end product

<script type="text/javascript" src="https://www.google.com/jsapi"></script>  

<script type="text/javascript">  
    google.load("visualization", "1", {packages:["corechart"]})
    google.setOnLoadCallback(drawChart);
    function drawChart() {
        var data = new google.visualization.DataTable({"cols": [{"type": "number" ,"id": "Column 1" ,"label": "Column 1" }, {"type": "number" ,"id": "Try" ,"label": "Try" }], "rows" : [{"c" : [{"v": 0}, {"v": 15}]}, {"c" : [{"v": 0}, {"v": 33}]}, {"c" : [{"v": 0}, {"v": 48}]}, {"c" : [{"v": 0}, {"v": 54}]}, {"c" : [{"v": 0}, {"v": 74}]}, {"c" : [{"v": 1}, {"v": 54}]}, {"c" : [{"v": 2}, {"v": 5}]}, {"c" : [{"v": 2}, {"v": 19}]}, {"c" : [{"v": 2}, {"v": 32}]}, {"c" : [{"v": 2}, {"v": 39}]}, {"c" : [{"v": 2}, {"v": 61}]}, {"c" : [{"v": 2}, {"v": 69}]}, {"c" : [{"v": 3}, {"v": 34}]}, {"c" : [{"v": 3}, {"v": 59}]}, {"c" : [{"v": 3}, {"v": 73}]}, {"c" : [{"v": 3}, {"v": 80}]}, {"c" : [{"v": 4}, {"v": 20}]}, {"c" : [{"v": 4}, {"v": 54}]}, {"c" : [{"v": 4}, {"v": 61}]}, {"c" : [{"v": 4}, {"v": 72}]}, {"c" : [{"v": 5}, {"v": 7}]}, {"c" : [{"v": 5}, {"v": 19}]}, {"c" : [{"v": 5}, {"v": 23}]}, {"c" : [{"v": 5}, {"v": 36}]}, {"c" : [{"v": 5}, {"v": 43}]}, {"c" : [{"v": 5}, {"v": 46}]}, {"c" : [{"v": 5}, {"v": 69}]}, {"c" : [{"v": 6}, {"v": 65}]}, {"c" : [{"v": 6}, {"v": 78}]}, {"c" : [{"v": 7}, {"v": 15}]}, {"c" : [{"v": 7}, {"v": 21}]}, {"c" : [{"v": 7}, {"v": 47}]}, {"c" : [{"v": 7}, {"v": 49}]}, {"c" : [{"v": 7}, {"v": 67}]}, {"c" : [{"v": 8}, {"v": 7}]}, {"c" : [{"v": 8}, {"v": 10}]}, {"c" : [{"v": 8}, {"v": 22}]}, {"c" : [{"v": 8}, {"v": 35}]}, {"c" : [{"v": 8}, {"v": 46}]}, {"c" : [{"v": 8}, {"v": 66}]}, {"c" : [{"v": 9}, {"v": 3}]}, {"c" : [{"v": 9}, {"v": 8}]}, {"c" : [{"v": 9}, {"v": 25}]}, {"c" : [{"v": 9}, {"v": 36}]}, {"c" : [{"v": 9}, {"v": 38}]}, {"c" : [{"v": 9}, {"v": 45}]}, {"c" : [{"v": 9}, {"v": 47}]}, {"c" : [{"v": 9}, {"v": 50}]}, {"c" : [{"v": 9}, {"v": 57}]}, {"c" : [{"v": 9}, {"v": 77}]}, {"c" : [{"v": 10}, {"v": 25}]}, {"c" : [{"v": 10}, {"v": 28}]}, {"c" : [{"v": 10}, {"v": 42}]}, {"c" : [{"v": 11}, {"v": 17}]}, {"c" : [{"v": 11}, {"v": 52}]}, {"c" : [{"v": 11}, {"v": 69}]}, {"c" : [{"v": 11}, {"v": 71}]}, {"c" : [{"v": 12}, {"v": 9}]}, {"c" : [{"v": 12}, {"v": 29}]}, {"c" : [{"v": 12}, {"v": 32}]}, {"c" : [{"v": 12}, {"v": 67}]}, {"c" : [{"v": 13}, {"v": 3}]}, {"c" : [{"v": 13}, {"v": 7}]}, {"c" : [{"v": 13}, {"v": 21}]}, {"c" : [{"v": 13}, {"v": 32}]}, {"c" : [{"v": 13}, {"v": 51}]}, {"c" : [{"v": 13}, {"v": 58}]}, {"c" : [{"v": 13}, {"v": 80}]}, {"c" : [{"v": 14}, {"v": 36}]}, {"c" : [{"v": 14}, {"v": 41}]}, {"c" : [{"v": 14}, {"v": 57}]}, {"c" : [{"v": 14}, {"v": 59}]}]});

        var options = {"colors":["red"],"hAxis":{"gridlines":{"count":15},"title":"Match"},"legend":{"position":"right"},"title":"Minutes tries conceded","vAxis":{"gridlines":{"count":10},"title":"Minute","viewWindow":{"max":80}},"bubble":{"textStyle":{"color":"transparent"}}} 

        var chart = new google.visualization.ScatterChart(document.getElementById('1253df25-ada1-42de-a30d-935828ed4439'));
        chart.draw(data, options);
    }
</script>

<div id="1253df25-ada1-42de-a30d-935828ed4439"  style="width: 700px; height: 300px;"></div>

## How to build it

The first thing to do is fire up vscode and install the ionide-fsharp and ionide-paket extensions, if you've not already done so.

Hit `ctrl` + `shift` + `p` to show all commands and run:

* Paket: Init
* Paket: Add Nuget Package -> FsLab

Then add a new .fsx file and reference the required packages:

```
#r "packages/FSharp.Data/lib/net40/FSharp.Data.dll"
#r "packages/XPlot.GoogleCharts/lib/net45/XPlot.GoogleCharts.dll"
#r "packages/Google.DataTable.Net.Wrapper/lib/Google.DataTable.Net.Wrapper.dll"

open System.IO  
open FSharp.Data  
open XPlot.GoogleCharts
```

The data has been sourced from various match reports. Starting with a subset of data this will be read in from an external JSON file, consisting of an array of rugby matches:

```json
    {
        "opposition": {
            "name": "TheTeamName",
            "tries": [
                {"name":"ThePlayerName", "minute":1}
            ]
        }
    }
```

Read the JSON using the JSON Type Provider

```
type Matches = JsonProvider<"matches.json">

let matches =  
    Matches.GetSamples()
```

Points is a list of tuples of type (int, int). The first int is the rugby match, the second is the minute the try is scored.

```
let points =  
    [for matchIndex in 0..Seq.length matches-1 do
        let theMatch = matches |> Seq.item matchIndex
        let tries = theMatch.Opposition.Tries
        for tryIndex in 0..Seq.length tries-1 do
            let theTry = tries |> Seq.item tryIndex
            yield (matchIndex, theTry.Minute)]
```

Set graph options:

```
let options =  
    Options(
        title = "Minutes tries conceded",
        hAxis = Axis(title = "Match", gridlines = Gridlines(count=matches.Length)),
        vAxis = Axis(title = "Minute", gridlines = Gridlines(count=10), viewWindow = ViewWindow(max=80)),
        bubble = Bubble(textStyle=TextStyle(color="transparent")),
        colors = [| "red" |] )
```

Create a scatter chart from the points defined above and launch in browser:

```
let chart =  
    points
    |> Chart.Scatter
    |> Chart.WithOptions options
    |> Chart.WithLabels ["Try"]
    |> Chart.WithSize (800, 300)
    |> Chart.Show
```

## What next?

* Create other visualisations using the full set of data
* Explore trends in the visualisations
