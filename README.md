# ROCO
The **RO**udanbout traffic **CO**nflict Dataset is a collection of traffic conflict events
 recorded at the two-lane roundabout at the intersection of State St. and W. Ellsworth Rd. in Ann Arbor, Michigan.
 Each event captures a 30-second duration of the conflict.
 The dataset provides the trajectories of the conflicts, 
 along with information about the reason, time, and effect of conflict.

- The data was collected from 9am to 6pm in July 2023.
- The data sample rate is 2.5Hz.
- MSight roadside perception system is used to extract the vehicle trajectories from raw video frames.

A related dataset: [RBTrajectoryData](https://github.com/michigan-traffic-lab/RBTrajectoryData)
provides more trajectory data in July 2023 at the same roundabout.
## Citation
> [ROCO: A Roundabout Traffic Conflict Dataset](https://arxiv.org/abs/2303.00563)<br />
> Depu Meng, Owen Sayer, Rusheng Zhang, Shengyin Shen, Houqiang Li, and Henry X. Liu<br />
> *Transportation Research Board Annual Meeting, 2023*
> ```
> @article{zhang2022design,
>     author = {Meng, Depu and Sayer, Owen and Zhang, Rusheng and Shen, Shengyin and Li, Houqiang and Liu, Henry X.},
>     title ={ROCO: A Roundabout Traffic Conflict Dataset},
>     journal = {Transportation Research Board Annual Meeting},
>     year = {2023},
> }
> ```

## Sample Set
For this release, we are providing a sample set of traffic conflict events from one week.
These events were selected to provide a representative sample of the full dataset.
Each event is stored as a separate folder in the dataset.

## Data Format
### Data directory structure
The dataset is formatted into a zip file. The structure of the dataset is:
```
root/
    |- label.csv    # the label file of the dataset
    └- data/    # the raw trajectory data
        |- 2023-07-10_18-31-30     # the trajectory data for one conflict event
        |   |- 2023-07-10 18-31-30-110186.json     # the trajectory file of one frame
        |   |- 2023-07-10 18-31-30-520815.json     # the trajectory file of one frame
        |   ...
        |- 2023-07-11_13-43-54
        ...
```

### Label format
In the label CSV file, it contains the following fields:
- Severity: A level either 1 or 2 that indicates the severity of the traffic conflict
    - level 1 - a near-miss event
    - level 2 - a traffic accident
- Reason: A label that describes the reason for the traffic conflict.
    - 0 - entering a roundabout without yielding to the circulating vehicles
    - 1 - unnecessary stop in the circle
    - 2 - improper lane use
    - 3 - secondary conflicts. The conflict is caused by previous events, like a previous conflict or previous crash
    - 4 - others
- The effect of the conflict on the traffic flow:
    - 0 - the traffic flow is not affected
    - 1 - one or two vehicles are forced to slow down in the circle due to the conflict
    - 2 - one or two vehicles are forced to stop in the circle due to the conflict
    - 3 - three or more vehicles are forced to slow down or stop in the circle due to the conflict

In the CSV file, the columns are:
```
event_timestamp,severity,reason,conflict trajectory pair,effect,time offset
```

### Trajectory format
The trajectory file is a JSON file that contains the trajectory of one frame.
Here is an example of the data in a json file
```
[
  {
    "id": "1",    # id of the vehicle (not universal unique id)
    "confidence": 0.849,    # confidence of the vehicle detection
    "lat": 42.301,    # the latitude coordinate of the vehicle position
    "lon": -83.698,   # the longitude coordinate of the vehicle position
    "uuid": "d3175b38-4e73-42f9-abb3-564b05788e90",       # the universal unique id of the vehicle
    "category": 0.0,      # the category of the vehicle (0: cars, 1: truck/bus/trailer)
    "speed": 1.536,      # the speed of the vehicle (m/s)
    "speed_heading": -1.741,      # the heading of the vehicle (north: 0, clock-wise)
  },
]
```

## Download

## Terms of Use
### Licenses
Unless specifically labeled otherwise, these Datasets are provided to You under a Creative Commons Attribution-Sharealike 4.0 International Public License (“CC BY-SA 4.0”) The CC BY-SA 4.0 may be accessed at https://creativecommons.org/licenses/by-nc-sa/4.0/legalcode. When You download or use the Datasets from the Website or elsewhere, You are agreeing to comply with the terms of CC BY-SA 4.0 and also agreeing to the Dataset Terms. Where these Dataset Terms conflict with the terms of CC BY-SA 4.0, these Dataset Terms shall prevail.

## Acknowledgement
The dataset is supported by [Mcity](https://mcity.umich.edu/) and [National Science Foundation](https://www.nsf.gov/).

## Developers
Depu Meng (depum@umich.edu)

Rusheng Zhang (rushengz@umich.edu)

Boqi Li (boqili@umich.edu)

## Contact
Henry Liu (henryliu@umich.edu)

Sean Shen (shengyin@umich.edu)
