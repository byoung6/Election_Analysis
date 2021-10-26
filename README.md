## Election Analysis Project

1. Overview of Project

The purpose of the project is to document new data points from an previously provided CSV file. Originally, the CSV file was used to provide election results and a breakdown of each candidate's respective vote counts and percentage of share of votes overall. With this new project, the goal is to document each county's representation of the overall vote total, and show which county had the largest turn out.

2. Election Audit Results

The election results are broken down in the following bullets, with images.

  - How many votes were cast in this congressional election

Using the following function, we find the total votes in the congressional election amounted to 369,711.
```
for row in file_reader:
        total_votes += 1

    #print candidate names
        candidate_name = row[2]

    #add to list
        if candidate_name not in candidate_options:
        #add to list
            candidate_options.append(candidate_name)

            candidate_votes[candidate_name] = 0
        candidate_votes[candidate_name] += 1
```
![The following print and text edit allows for this screenshot](https://user-images.githubusercontent.com/76926631/138788031-2d8eb7f3-b5ff-443e-98b0-3e95c97c12d3.PNG)

```
with open(file_to_save, "w") as txt_file:
    # After opening the file print the final vote count to the terminal.
    election_results = (
        f"\nElection Results\n"
        f"-------------------------\n"
        f"Total Votes: {total_votes:,}\n"
        f"-------------------------\n")
    print(election_results, end="")
    txt_file.write(election_results)
```

   - Breakdown of the number of votes and the percentage of total votes in each precinct
The breakdown of the number of votes and the percentage of total votes in each precinct was determined through the following for loop:
```
    for county_name in county_votes:
        # 6b: Retrieve the county vote count.
        c_votes = county_votes.get(county_name)
        # 6c: Calculate the percentage of votes for the county.
        county_percentage = float(c_votes) / float(total_votes) * 100

         # 6d: Print the county results to the terminal.
        county_results = (
        f"{county_name}: {county_percentage:.1f}% ({c_votes:,})\n")
        print(county_results)
         # 6e: Save the county votes to a text file.
        txt_file.write(county_results)
```
This results in the breakdown of:
    Jefferson: 10.5% (38,855)
    Denver: 82.8% (306,055)
    Arapahoe: 6.7% (24,801)

   - Denver had the largest turnout
The breakdown of the largest turnout was determined through the use of a separate dictionary and list, and associated for loop, conditioning upon the following parameters:
```
            largest_count = c_votes
            largest_percentage = county_percentage
            largest_county = county_name
```
This brings up Denver as the largest turnout

   - Breakdown of the number of votes and percentage of votes for each candidate
The breakdown of the votes and percentage of the votes per candidate equals to:

     - Charles Casper Stockham: 23.0% (85,213)
     - Diana DeGette: 73.8% (272,892)
     - Raymon Anthony Doane: 3.1% (11,606)

![candidate results](https://user-images.githubusercontent.com/76926631/138788056-5ea32ddf-6546-4515-8c44-8b81793eaf85.PNG)

   - Winner and by how much
The winner of the election was Diana DeGette with 272,892 votes, with the next closest at 85,213 total votes. 


3. Election Audit Summary

The pypoll script can be used regardless of number of candidates, as it will automatically pull all candidate information from a given CSV file. It will also provide the aforementioned breakdowns in a separate txt file to provide more indepth information. Furhter improvements that can be made to the script can include breakdown per candidate per county, wherein we can see what percentage of each county voted for which specific candidate. This can have further implications as to which county holds certain political views. In order to implement this change, another for loop will need to be implemented cross referencing the already existing vote count totals per county, per candidate. 
